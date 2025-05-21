# Lessons Learned

> **Instruction for AI Agents:**  
> When generating new code, always review and apply the lessons below. These are distilled best practices and common pitfalls.
> - Before producing code, check if any lesson applies to your output.
> - If a lesson is relevant, ensure your code follows the "Do" example and avoids the "Don't".
> - If you are unsure, prefer the "Do" approach.

> **How to add an entry:**  
> - Use a clear, numbered heading for each lesson (e.g., `### 1. Title of Lesson`).
> - Briefly describe the issue or best practice.
> - Use **Don't:** and **Do:** code blocks to illustrate incorrect and correct usage.
> - Add notes or explanations as needed.
> - Keep entries concise and focused on actionable advice.

---

## Pydantic Model Usage: Key Lessons

This document summarizes best practices and common pitfalls when working with Pydantic models in Python projects.

---

### 1. Pydantic Models Are Not Dictionaries

- **Don't:**  
  ```python
  step['response'] = "Some result"  # ❌ Raises TypeError
  ```
  > `TypeError: 'SomePydanticModel' object does not support item assignment`

- **Do:**  
  - Assign to fields using attribute syntax:
    ```python
    step.response = "Some result"  # ✅ Correct
    ```
  - If you need to store new data, add the field to the model definition first:
    ```python
    # In schemas.py
    class PlanStep(BaseModel):
        step_id: str
        instructions: str
        response: Optional[str] = None  # Field must be defined
    ```

---

### 2. No `.get()` Method

- **Don't:**  
  ```python
  steps = plan.get("steps", [])  # ❌ Raises AttributeError
  ```
  > `AttributeError: 'SomePydanticModel' object has no attribute 'get'`

- **Do:**  
  ```python
  steps = plan.steps  # ✅ Correct
  ```

---

### 3. Serializing Pydantic Models to JSON

- **Don't:**  
  ```python
  json.dumps(my_instance)  # ❌ Raises TypeError
  json.dumps([my_instance1, my_instance2])  # ❌ Raises TypeError
  ```
  > `TypeError: Object of type 'YourPydanticModel' is not JSON serializable`

- **Do:**  
  ```python
  json.dumps(my_instance.model_dump())  # ✅ Correct for a single instance
  json.dumps([item.model_dump() for item in my_list])  # ✅ Correct for a list
  ```

---

### 4. Gemini API: Structured Output with Pydantic

- **Don't:**  
  Manually parse JSON from Gemini API responses when using a Pydantic `response_schema`:
  ```python
  # ❌ Not recommended
  json_string = resp.candidates[0].content.parts[0].text
  parsed_json = json.loads(json_string)
  my_object = MySchema(**parsed_json)
  ```

- **Do:**  
  Use the built-in `.parsed` attribute:
  ```python
  parsed_object = resp.parsed
  if parsed_object is None:
      # Handle parse failure (e.g., check resp.prompt_feedback)
      raise ValueError("Gemini API's resp.parsed was None.")
  if not isinstance(parsed_object, MySchema):  # Or List[MySchema]
      raise TypeError("Parsed object is not of the expected schema type.")
  # Use parsed_object as your validated Pydantic instance(s)
  ```

  > **Note:** If `resp.parsed` is `None`, check `resp.prompt_feedback` or `resp.candidates[0].finish_reason` for error details.

---


[<< Back](./react.md)

# React Hook Form

- `useForm()`: returns a form object where you can use it to manage your form.

- the steps to create a form using react-hook-form is as follows:

  1. you have to define a type that represents the form i.e.:

  ```js
  type LoginForm = {
    username: string,
    password: string,
  };
  ```

  2. call the `useForm` hook: `const form = useForm<LoginForm>()`
  3. call the `form.register` function for each field in your form:

  ```js
  const emailField = form.register("email");
  const passwordField = form.register("password");
  ```

  4. create the jsx elements that will represent your form and spread the field object in the input:

  ```js
  return (
    <input type="text" id="email" {...emailField}>
    <input type="text" id="password" {...passwordField}>
  )
  ```

  5. on the form tag you have to call handleSubmit and pass it a submit function:

  ```js
  const onSubmit = (data: LoginForm) {
    //do something with data
  }
  // code ...
  return <form onSubmit={form.handleSubmit(onSubmit)}>...</form>
  ```

- you can specify default values inside the `useForm` call

```js
const form = useForm<...>({
  defaultValues: {
    email: "example@gmail.com",
  },
});
```

- you can add validation on fields by passing them to the register function
- there are different kind of validation

  - built-in validation(required)
  - custom validations
  - async validations

- **built-in validation**:

```js
form.register("email", {
  required: "this field is required",
  pattern: { value: /.*@.*\.com/, message: "enter a valid email" },
});
```

- **custom validations**:

```js
form.register("password", {
  validate: {
    strongPassword: (password) => {
      // do some logic and return true or error message
      if (password.length < 6) return "password too short";
      return true;
    },
  },
});
```

- **async validation**

```js
form.register("email", {
  validate: {
    emailDoesnotExist: async () => {
      // await for requests
      return true;
    },
  },
});
```

- you can change when the validation is triggered using the mode field in `useForm({mode: "onBlur"})`

- you can add devtool by appending this after your form jsx:

```js
<DevTool control={form.control}>
```

- for each field, if it is:

  - **touched**: this means that the user clicked on the field and clicked away
  - **dirty**: this means that the user has typed something.

- you can access the errors for each field by `form.formState.errors.username?.message`

- you can reset the form by `form.reset()`
- `reset` can take an object that will be used as the default values for the fields
- only the fields that are explicitly registered by `register('field')` will take a default value from the object passed to reset. if there are values that was set by `setValue` these will be deleted.
- you can add nested Object in your form definition

```js
const FormType = {
    field: {
        A: string;
        B: string;
    }
}
<input {...form.register("field.A")}>
<input {...form.register("field.B")}>
```

- you can add fixed size arrays in your from definition

```js
const FormType = {
    field: string[];
}
<input {...form.register("field.0")}>
<input {...form.register("field.1")}>
```

- you can add dynamic size arrays in your form definition

```js
const FormType = {
   phoneNumbers: {number: string}[]
};

const dynamicField = useFieldArray({
  name: "phoneNumbers",
  control: form.control,
});

return (
  <div>
    {
      dynamicField.map((field, index)=> (
        <div key={field.id}>
          <input {...form.register(`phNumbers.${index}.number`)}>
          <button type="button" onClick={()=>dynamicField.remove(index)}>Remove</button>
        </div>
      ))
    }
    <button type="button" onClick={()=>dynamicField.append({number:""})}>Add</button>
  </div>
)
```

- to use date values in form as date object instead of string you have to add `valueAsDate: true` in the register options object

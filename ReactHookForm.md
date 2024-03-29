# React Hook Form

1. What is React Hook Form ?  
   R: Library for React and React native that allows you to manage form data and submition. It also adds validation options.

2. What is the `register` method from the `useForm` hook ?  
   R: It is a function that allows you to pass data to your form inputs.

   Example:

   ```tsx
   <input type="number" {...register("age", { min: 18, max: 99 })} />
   ```

3. Can you register your own Input components ?  
    R: Yes, there is a way with ref and another way by using a `register` prop.

   Example:

   ```tsx
   const Input = ({ label, register, required }) => (
     <>
       <label>{label}</label>
       <input {...register(label, { required })} />
     </>
   );
   ```

4. Does it work with third party Inputs ?  
    R: Yes, you can pass the register if the input component exposes a ref to its input element.

   If that is not the case you can also use the `Controller` component that will help you to obtain control of the input element:

   ```tsx
   <Controller
     name="firstName"
     control={control}
     render={({ field }) => <Input {...field} />}
   />
   ```

5. Can the form values be redux global states ?  
    R: Yes, you have to use the `connect` method from redux to make this possible.

   ```ts
   connect(
     ({ firstName, lastName }) => ({ firstName, lastName }),
     updateAction
   )(YourForm);
   ```

6. Does this library manages validation ?  
   R: Yes it does. You can pass the validation for each value using the second parameter of the `register` function.

   ```tsx
   {...register("firstName", { required: true })}
   ```

7. Can the library help you with doing direct REST requests from the form ?  
   R: Yes, here you have an example:

   ```tsx
   <Form
     action="/api/save" // Send post request with the FormData
     // encType={'application/json'} you can also switch to json object
     onSuccess={() => {
       alert("Your application is updated.");
     }}
     onError={() => {
       alert("Submission has failed.");
     }}
     control={control}
   >
     <input {...register("firstName", { required: true })} />
     <input {...register("lastName", { required: true })} />
     <button>Submit</button>
   </Form>
   ```

8. Can you use schema validation from other libraries (like yup) ?  
   R: Yes, you can use the schema validation from third party libraries like yup. Here you have an example:

```tsx
const schema = yup
  .object({
    firstName: yup.string().required(),
    age: yup.number().positive().integer().required(),
  })
  .required();

export default function App() {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm({
    resolver: yupResolver(schema),
  });
  const onSubmit = (data) => console.log(data);

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("firstName")} />
      <p>{errors.firstName?.message}</p>

      <input {...register("age")} />
      <p>{errors.age?.message}</p>

      <input type="submit" />
    </form>
  );
}
```

## Basic Example

```tsx
import { useForm, SubmitHandler } from "react-hook-form";
interface IFormInput {
  firstName: string;
  lastName: string;
  age: number;
}
export default function App() {
  const { register, handleSubmit } = useForm<IFormInput>();
  const onSubmit: SubmitHandler<IFormInput> = (data) => console.log(data);
  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("firstName", { required: true, maxLength: 20 })} />
      <input {...register("lastName", { pattern: /^[A-Za-z]+$/i })} />
      <input type="number" {...register("age", { min: 18, max: 99 })} />
      <input type="submit" />
    </form>
  );
}
```

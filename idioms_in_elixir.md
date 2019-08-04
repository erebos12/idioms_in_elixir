# Idioms and Patterns in Elixir

## Composing functions by Pipe-Operator
Combining functions with `|>` operator:

    def function_name(input) do
      input
      |> process_input_1
      |> process_input_2
    end

The argument for the pipe operator is always the first argument of the function.


## Return a tuple in a function
As return value of a function use a tuple which holds the state and the value of the function.

    { :ok, value } # --> for success
    { :error; %{ reason: "an error message here"} }  # --> for error

The caller can then use pattern matching to control the flow in case of success or error. See '_**Control-Flow with Pattern-Matching**_'.

## Control-Flow with Pattern-Matching
Use Pattern-Matching to control the flow instead of if-then-else or case-statement.

    def function_name(file) do
      {:ok, file} ->
        IO.write(file, "Hello World!")
        File.close(file)

      {:error, error} ->
        IO.puts("Error occurred ...")
    end

## Functions guards
Use function guards to check for constraints on functions arguments:

    def check(x) when is_atom(x) do
       ... # do something here
    end

## Pattern Matching in function arguments
When arguments are passed to a function, use pattern matching to extract required values:

    defmodule PersonInfo do
      def age_of_person(%{age: age_of_person}) do
        IO.puts "The person is " <> age_of_person
      end
    end

    alex = %{ name: "Alex", age: 40, role: "Software Developer" }
    PersonInfo.age_of_person(alex)
    "The person is 40"


## def instead of case-statement
Use functions with argument Pattern-matching instead of case-statement

    def format_response(code, message) do
       case code do
         200 -> nil
         404 -> "Not found"
         500 -> "Boom"
       end
    end

This can be written with functions:

    def format_response(200, _message), do: nil
    def format_response(404, message), do: "Not found"
    def format_response(500, message), do: "Boom"

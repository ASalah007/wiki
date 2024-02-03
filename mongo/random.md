# Random

- there are query operators and aggregate operators in mongodb
- when there is a single condition inside $elematch you can omit it.

  ```js
    {
        arrayField: {
            $elematch: {
                objectField: <exp>
            }
        }
    }
    ==
    {
        arrayField.objectFiled: <exp>,
    }

  ```

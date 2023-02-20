# Serializers

- basic serializer

```
from rest_framework import Serializer

class Ser(serializers.Serializer):
    field = serializer.CharField(max_length=200)
    ...

    def create(self, validated_data):
        #create the objects

    def update(self, instance, validated_data):
        #update the instance
```

- if you want to add attributes that is not part of the requestd data but required by the object, theses attributes will be added to the validated_data:

```
serializer.save(attr=val)
```

- when you call the is_valid() method and validation errors occured. the serializer.errors will contain a dictionary i.e. {"field": ["error", "error"]}

- is_valid(raise_exception=True) -> returns HTTP 400 BadRequest if there is any ValidationError while validating

- you can add custom validator functions on any field by declaring validate_field_name() function in the serializer,  
  this function must either return the **validated data** or raise **ValidationError**

```
from rest_framework import serializers

class BlogPostSerializer(serializers.Serializer):
    title = serializers.CharField(max_length=100)

    def validate_title(self, value):
        if 'django' not in value.lower():
            raise serializers.ValidationError("Blog post is not about Django")
        return value
```

- if you want to validate multible fields together you can declare a **validate(self, fields)** function that accepts a dictionary of the fields and it also must either return the dictionary or raise ValidationError

- serializers classes are also of type Field you can use Serializer class to represent nested objects of different relations
```
class CommentSerializer(serializers.Serializer):
    user = UserSerializer(required=False) 
    content = serializers.CharField(max_length=200)
    created = serializers.DateTimeField()
```
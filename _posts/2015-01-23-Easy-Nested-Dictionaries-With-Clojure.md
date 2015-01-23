---
layout: post
title: Easy Nested Maps ith Clojure
published: false
---

## Easy Nested Maps with Clojure

Clojure has some really great functions in its core library for dealing with getting and updating values in [Maps](http://clojure.org/data_structures#Data%20Structures-Maps%20%28IPersistentMap%29) (Clojure’s set of key/value based data structures). In particular, I’ve realised that the [get-in](https://clojuredocs.org/clojure.core/get-in) function is particularly useful. I used to just think of it as syntactic sugar, but, it's actually a great help in simplifying code and separating conerns.

### Feeling the Pain

In a lot of contemporary programming languages, if you attempt to use a non-existent key on a dictionary things will blow up. In Python (where we have [dicts](https://docs.python.org/3.4/library/stdtypes.html#dict)): 


```
example_dict = {"house": "foo"}

print(example_dict["house"]) 
	=> foo

print(example_dict["car"])
	=> 	Traceback (most recent call last):
  		File "<stdin>", line 1, in <module>
		KeyError: 'car'
```

This isn’t necessarily bad, but, it is often unnecessary. It will create a compound problem when you are working with nested dictionaries. For example, I might be working with some parsed JSON from an external source. If that JSON has some optional values I'm going to start feeling a lot of pain if I need to start adding key checks for all the optional values.

In a lot of cases, we might be totally fine with this optional values not being set. This means we’ve written code to check whether or not a key exists so that we can end up not caring it doesn’t exist.

It starts to become difficult to manage all those key existence checks, so, something like this gets implemented to deal with it. 

```
json_dict = {
	"image_url": "http://imgur.com/r/cats/1uLxCpW",
	"user_details": {
		"name": "Mr Cat",
		"age": 10
	}
}

def get_nested_value_in_dict(nested_key, d):
	keys = nested_key.split(" ")
	current_val = d
	for key in keys:
		if key in current_val:
			current_val = current_val[key]
		else:
			return None
	return current_val

print(get_nested_value_in_dict("user_details name", json_dict))
	=> Mr Cat

print(get_nested_value_in_dict("user_details eye_colour", json_dict))
	=> None
```

This isn’t a lot of code; it’s straightforward and it works. However, it also adds another convention to the codebase. Every time we add a new convention we need to learn it, everyone else needs to learn it and then when we move to another project we have to potentially unlearn it. Even if you are using a library to deal with nested dictionaries, that's still an additional thing to think about and maintain.

### Getting Unexceptional

In Clojure we can do the usual look up of a single key in a Map:

```
(def example-map {:house "foo"})

(:house example-map)
	=> "foo"

(:car example-map)
	=> nil
```

If the key doesn't exist, we get a nil not an exception. The [get-in](https://clojuredocs.org/clojure.core/get-in) for nested Maps also returns nil:

```
(def json-map
  {
  	:image-url "http://imgur.com/r/cats/1uLxCpW"
   	:user-details {
                   	:name "Mr Cat"
                    :age 10
                   }})

(get-in json-map [:user-details :name])
	=> "Mr Cat"
(get-in json-map [:user-details :eye-colour])
	=> nil
```

This is a core function in Clojure. It is the standard way of accessing nested values in Clojure Maps. Across all Clojure projects. If I see this, I know immediately what the intent of the code is. 

The function returns nil when a key doesn’t exist (or when the value accessed was nil). No exceptions are thrown - it’s for me to decide if the non-existence of a value I was looking for is considered exceptional behaviour. 

### So What?

This unexceptional behaviour might not always be what you want. Maybe you are interested in very strict access to the values in a Map, but, and you will need to explicitly add that behaviour. However, the separation of accessing values and caring about whether they exist or not can be very liberating in a lot of circumstances.

By leaning on core functionality and convention in this way, our code can get much more readable and our intent more immediately obvious. This lets us spend time writing behavour we want instead of boilerplate.
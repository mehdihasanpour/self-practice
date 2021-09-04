# Late Static Binding in PHP
``` php 
class Animal {
    protected $name = 'Animal';

    public function getName() {
        return $this->name;
    }
}
```

Let's extend the Animal class so we can use its getName() method without repeating it in child class. We will only need the $name variable in child class to get it's name:
``` php 
class Cat extends Animal {
    protected $name = 'Cat';
}
```

Now we expect to get names of each object, let's do so:
``` php 
$animal = new Animal;
$cat = new Cat;

echo $animal->getName(); // Animal
echo $cat->getName(); // Cat
```

And we successfully get Animal and Cat echoed out. But now let's modify code a bit so that we can use those classes without creating their instances with the help of static keyword (eg global state):
``` php 
class Animal {
    protected static $name = 'Animal';

    public static function getName() {
        return self::$name;
    }
}

class Cat extends Animal {
    protected static $name = 'Cat';
}

echo Animal::getName(); // Animal
echo Cat::getName(); // Animal
```

## By Using static keyword

``` php 
class Animal {
    protected static $name = 'Animal';

    public static function getName() {
        return static::$name;
    }
}


class Cat extends Animal {
    protected static $name = 'Cat';
}

echo Animal::getName(); // Animal
echo Cat::getName(); // Cat
```
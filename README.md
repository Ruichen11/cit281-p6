# CIT281 Project-6

Purpose of this project:
- Gain experience creating and working classes with inheritance
- Gain more experience debugging code 
- Gain more experience writing and executing non-web server Node.js JavaScript code using VSCode

Overview:
- Create 3 classes. First class is the shape class that will serve as the base class for the other two classes.
- second class is the rectangle class that will inherit from shape class
- third class is the triangle class

## Project Code

### Shape Class
- Name the class Shape
- Provide a constructor that expects an array of sides, with a default value of an empty array []
- Create a class property sides that contains the constructor sides array using the this object
- Implement a class method perimeter that returns the value of the lengths of all sides.
- You may want to create this method initially using whatever version of a function you prefer, and once complete refactor the function using the remaining requirements
- This method must use an implicit arrow/lambda function
- You must use the Array reduce() method to calculate the perimeter value
- To make this method a single line of code, you will also need to use the ternary operator ( ? : ) to make sure the array has at least one side

```
class Shape {
    constructor(sides = []) {
        this.sides = sides;
    }
    perimeter = () => this.sides.length > 0 ? this.sides.reduce((sum, x) => sum + x) : 0
}
```

### Rectangle Class
- The Rectangle class inherits from the Shape class using the extends operator. 
- Name the class Rectangle
- Provide a constructor that expects two parameters length and width with default values of 0
- Call the parent class Shape constructor using the super() method, and an array that consists of length, width, length, width, as a rectangle has four sides
- Create class properties length and width from the constructor parameters using the this object
- Implement a method area that returns the rectangle area, remembering that the area of a rectangle is length multiplied by width

```
class Rectangle extends Shape {
    constructor(length = 0, width = 0) {
        super([length, width, length, width]);
        this.length = length;
        this.width = width;
    }
    area = () => this.length * this.width;
}
```
### Triangle Class
- the Triangle class inherits from the Shape class using the extends operator. 
- Name the class Triangle
- Provide a constructor that expects three parameters sideA, sideB, and sideC with default values of 0
- Call the parent class Shape constructor using the super() method, and an array that consists of sideA, sideB, and sideC
- Create class properties sideA, sideB, and sideC from the constructor parameters using the this object
- Implement a method area that returns the triangle area, using [Heron's formula](https://www.mathsisfun.com/geometry/herons-formula.html) noting - that implementing this formula will require using Math.sqrt()

```
class Triangle extends Shape {
    constructor(sideA = 0, sideB = 0, sideC = 0) {
        super([sideA, sideB, sideC]);
        this.sideA = sideA;
        this.sideB = sideB;
        this.sideC = sideC;
    }
    area = () => {
        const s = this.perimeter() / 2;
        return Math.sqrt(s * (s - this.sideA) * (s - this.sideB) * (s - this.sideC));
    }
}
```
### Creating a generic block of code for processing an array of sides arrays. 

 Requirements:
- for..of to iterate through the array
- variable initialization to null as a variable to hold the object created using new
- switch() to branch based on number of sides (2, 3 and default for all other values)
- spread/scatter ellipsis to pass the side array as individual values
- template literal for the output
- Array toString() method to produce a string of values from an array separated by commas

```
const data = [ [3, 4], [5, 5], [3, 4, 5], [10], [] ];

for (const sides of data) {
    let description = "";
    let shape = null;
    switch (sides.length) {
        case 2:
            description = "Rectangle";
            if (sides[0] === sides[1]) {
                description = "Square";
            }
            shape = new Rectangle(...sides);
            break;
        case 3:
            description = "Triangle";
            shape = new Triangle(...sides);
            break;
        default:
            break;
    }
    if (description.length > 0) {
        console.log(`${description} with sides ${sides.toString()}` +
        ` has perimeter of ${shape.perimeter()}` + 
        ` and area of ${shape.area()}`);
    } else {
        const plural = sides.length !== 1 ? 's' : '';
        console.log(`Shape with ${sides.length} side${plural} unsupported`);
    }
}

```
### Expected Output
![P6 SC](https://user-images.githubusercontent.com/84296093/120622940-1e334a80-c414-11eb-8c04-79ce900a59cb.JPG)


[SourceCode](https://ruichen11.github.io/Ruichen11.CIT-Minor/)

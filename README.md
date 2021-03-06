# Generate Image Avatars with Initials in JavaScript
Avatars create a digital representation of a user and are usually used in web profiles. Most of the time a user is required to upload an image then used as the profile. An example of this is Google Mail Services. When a user does not upload a profile image an avatar is generated using his/her initials. Are you curious of how this magic happens? Don’t worry I’ve got you covered. 

In this article we are going to explore how we can generate avatars based on user initials.

## Github

Check out the complete source code in this  [GitHub Repository](https://github.com/874bowen/Avatars-JavaScript.git).

## Pre-requisites
To follow along through this article you are required to have: 
- Basic knowledge of HTML
- Knowledge in Javascript
- Some knowledge in Bootstrap

## Introduction
In this article we are going to use HTML5, Bootstrap UI framework and JavaScript to create an application that allows users to generate avatars using their names and the colors of their choice.

## Sample Project Setup
In this article I will need you to clone the project from GitHub
```bash
git clone https://github.com/874bowen/Avatars-JavaScript.git
cd Avatars-JavaScript
```
In your favorite text editor open the `Avatars-JavaScript` folder then right click `index.html` and open the file in your browser. You should be able to see this page after you enter your name, choose favorite colors and click generate.

![img_1.png](https://res.cloudinary.com/bowenivan/image/upload/v1655558650/img_1_e0ymjz.png)

## Usage
Let us now examine the `index.js` to understand the functionality behind this application. 

```javascript
function generateAvatar(
    text,
    foregroundColor = "white",
    backgroundColor = "black"
) {
    const canvas = document.createElement("canvas");
    download = document.getElementById("download");
    const context = canvas.getContext("2d");

    canvas.width = 200;
    canvas.height = 200;

    // Draw background
    context.fillStyle = backgroundColor;
    context.fillRect(0, 0, canvas.width, canvas.height);

    // Draw text
    context.font = "bold 100px Assistant";
    context.fillStyle = foregroundColor;
    context.textAlign = "center";
    context.textBaseline = "middle";
    context.fillText(text, canvas.width / 2, canvas.height / 2 );
    download.href=canvas.toDataURL("image/png");
    return canvas.toDataURL("image/png");

}
```

### Create the Canvas Element
The `generateAvatar()` function takes three parameters that is the `text`, `foregroundColor` and `backgroundColor`. We are going to use createElement method to create a canvas element in our HTML document.

> createElement() method creates an element specified by tagName
> 
> HTML canvas is an element that can be used to draw graphics on a web page via scripting (usually JavaScript)

```javascript
const canvas = document.createElement("canvas");
```

### Draw the background
To get a drawing context on the canvas we use the `HTMLCanvasElement.getContext() `method and takes a contextType parameter `getContext(contextType)` for our case `"2d"` which leads to the creation of an object representing a  two-dimensional rendering context.

```javascript
const context = canvas.getContext("2d");
```

We can also specify the height pixels and width pixels of our canvas element by using the height and width attribute of the canvas element created.
```javascript
canvas.width = 200;
canvas.height = 200;
```

We can then draw our background by first setting the background color by using the `fillStyle` property then drawing a filled rectangle with the background set.

> The fillStyle canvas property sets the color used in filling the drawing.
>
> The fillRect() method draws a filled rectangle. Default background color is black.

The `fillRect()` takes four parameters, the x-coordinate of the upper corner of the rectangle, the y-coordinate of the upper corner of the rectangle, width of rectangle in pixels, and the height of the rectangle in pixels.

```javascript
// this is the syntax: context.fillRect(x, y, width, height);
// in our code context.fillrect(0, 0, 200, 200)
context.fillRect(0, 0, canvas.width, canvas.height);
```

### Draw the text
To draw the text inside our canvas element we have to set the font using the `font` property, fill the text with color using `fillStyle` property, text align our text using `textAlign` property, set the baseline used when drawing the text using `textBaseline` property and draw our text on the canvas using `fillText()` method.
```javascript
context.font = "bold 100px Assistant";
context.fillStyle = foregroundColor;
context.textAlign = "center";
context.textBaseline = "middle";
// context.fillText( text, x, y);
context.fillText(text, canvas.width / 2, canvas.height / 2 ); // (text, 100, 100)
```

We can then return a data URL containing the representation of the image in the format specified by the type parameter in our case `image/png`. To enable the user to download the avatar image we specify the target as the data URL of the image.

```javascript
download.href=canvas.toDataURL("image/png");
return canvas.toDataURL("image/png");
```

### Get inputs from user
We can get the values for full name, background color and text color from the user. so we can use them as arguments to the `generateAvatar()` method. The generate() method wil do this for us and will be called once the `generate` button is clicked.

```javascript
var name= document.getElementById("name").value;
var bcgColor= document.getElementById("bcg-color").value;
var textColor= document.getElementById("text-color").value;
```
After getting the name of our user we can get the  initials by first splitting the string using `split(" ")` then we get the first character from the first element and the last element. We then ensure that our initials are in uppercase.

```javascript
const myNames = name.split(" ");
const initials = myNames.shift().charAt(0) + myNames.pop().charAt(0);
const nameInitials =initials.toUpperCase();
```

Since we defined our avatar div to be of style `display:none` we can now show it and call the generateAvatar method passing the values from the user. 
```javascript
var avatarDiv = document.getElementById("avatarDiv");
if (avatarDiv.style.display === "none"){
    avatarDiv.style.display = "block";
}
document.getElementById("avatar").src = generateAvatar(
    nameInitials,
    textColor,
    bcgColor
);
```

## Conclusion
In this article, we have learnt how we can generate avatars based on the user's name. Its usefulness is the ability to automatically generate avatars even when user has not uploaded a profile image. 
This can be implemented in websites or apps that have the profile of a user once he/she has logged in.

# Merge images
#Image #Editing

Use the following command to stack two images above each other and scale the first image to have the same width as the seoncd:

```bash
magick convert -resize 1514x Image1.jpg Image2.jpg -append Output.jpg
```

Explanation of the command:
- **convert** => Part of the ImageMagick toolkit to convert images with endless options
`resize`$\quad$ This is used to scale Image 1 to have the same width as Image 2
`append`$\quad$Concatenates the images vertically
<br>  

An alternative way would be this:

```bash
magick convert -size 1514x1336 xc:white \
1.jpg -resize 1514x \
-gravity center -composite \
2.jpg -geometry +0+668 -composite \
output.jpg
```

Explanation of the command:
- **magick convert** => This is the command to convert and manipulate images with ImageMagick
`-size`$\quad$Creates a new blank image with a width of 1514 and a height of 1336 pixels, and fills it with white color. 
The height is set to 1336 because this is the total height of the final image, which is the sum of the heights of Image 1 and Image 2.
`image 1.jpg -resize 1514x`$\quad$Reads Image 1 from file 1.jpg and resizes it to have a width of 1514 pixels, keeping the aspect ratio. 
The resized image is then stored in memory as an image in the ImageMagick pipeline.
`-gravity center`$\quad$Places the resized Image 1 on top of the blank image, centered horizontally. 
`-composite`$\quad$Blends the two images together to create a single image. Since Image 1 is on top, it will appear above Image 2 in the final image.
`-image 2.jpg -geometry +0+668 -composite`$\quad$Reads Image 2 from file 2.jpg and places it in the bottom of the blank image, starting at position (0,668) (i.e., x=0, y=668). 
`output.jpg`$\quad$Specifies the output file name as `output.jpg`.
<br> 

The resulting image will have a width of 1514 pixels (matching the width of Image 2) and a height of 1336 pixels (the sum of the heights of Image 1 and Image 2).

## bat files for easy batch converting images with primtive

### what is it and why should i care?
it's a simple and dirty bat file i made for someone who needed to batch convert some of their images using [primitive](https://github.com/fogleman/primitive)

### how to use?
put your images in the "in" folder and use primtive.bat, after the process is complete the converted images can be found in the "out" folder

### what are magick.exe and convert.exe
these are part of the imagemagick program that primitve uses to make gif files out of the process, sort of like a before and after gif starting from a blank page and building the image up one shape at a time

### where did you get the binary or did you build it yourself from source
i did make a binary myself for my personal use but i used the binary that was made from another person on the internet for this repo

### something went wrong, how could i fix it?
i'll try to help if i can but my knowlege of the language is pretty limited so you are better served searching online

### what about linux?
i've uploaded a linux binary as well, make it executable if it's not already 
```
chmod +x primitive
```
either add the binary to a folder in your ```@PATH``` or put ```./``` behind the primitive binary in the folder it is in to let the shell know where it is, or put the absolute path to the binary like this ```~/bin/primitive```

install imagemagick for your distro

i'm planning on making a bash script eventually but you can use a simple bash/zsh function for the time being
```
primit () { for i in *.jpg; do echo $i; primitive -i $i -o p-$i."$1" -n "$2" -m "$3"; done; }
```
```-i``` imports images, change ```*.jpg``` to other extensions as needed or ```*.*``` if everything you have in a folder is pictures

```-o``` decides output extensions, if you want to output to different folders here is where to change it, like this: ```-o ./out/p-$i."$1"``` 

```-n``` decides number of the shapes, more is slower but makes the output image more similar to the input image

```-m``` sets the modes, ```0```for combo , ```1``` for triangle , ```2``` for rect , ```3``` for ellipse , ```4``` for circle , ```5``` for rotatedrect , ```6``` for beziers , ```7``` for rotatedellipse , ```8``` for polygon. multiple choices are not permitted here, choose one, for example ```-m 4```

after setting that function in your ```.bashrc``` or ```.zshrc``` open the terminal in a folder with your images and do this for example:
```
primit 500 1
```
above example converts every image with ```.jpg``` extension in your folder with traingle shape and 500 shapes per image


you can also do all of this in the terminal without making a function:
```
for i in *.jpg; do echo $i; primitive -i $i -o p-$i."png" -n "500" -m "1"; done
```
if you don't want to change output extension remove ```."png"``` part and just do ```-o p-$i```

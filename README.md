# Blender_Cheetah

This is a git repository for a Blender script to generate synthetic training data of random cheetah poses. The data is intended for use with DeepLabCut, and all annotations are saved in the relevant format. Currently, the program generates 2D pose information, 3D pose information, and basic camera information for a single camera. If you think of a better/more interesting name for this repo, please let me know. I am painfully uncreative when it comes to titles.

## 1    Installation

After you have downloaded or git cloned this repo, you will need to install Blender. The most recent version as of the writing of this text is Blender 2.81a; this is the version on which the code has been tested. You can download Blender for your operating system at https://www.blender.org/download/.

Once Blender is up and running, you will need to install this program's dependencies. There are only two:

* tables: https://pypi.org/project/tables/
* pandas: https://pypi.org/project/pandas/

... However, one does not simply pip install these dependencies. Blender ships with its own Python installation located inside the folder you should have downloaded from blender.org. Due to this, Blender cannot see any of the normally installed modules in your machine's own Python installation. Luckily, as of version 2.8, Blender ships with its own pip. Your only task is to locate this pip. Typically, it is found under yourdirectory/yourblenderfolder/2.81/python/bin/pip. Once you have found it, open a terminal instance and simply run:

    $ yourdirectory/yourblenderfolder/2.81/python/bin/pip install pandas
    $ yourdirectory/yourblenderfolder/2.81/python/bin/pip install tables

Pip should install both the required modules to Blender's Python installation. You can check if this was succesful by opening Blender, navigating to the Scripting panel, and running:

    import pandas
    import tables

If both imports run successfully, and no ModuleNotFound errors are thrown, you are good to go!

## 2    Before Running

The script works by rendering a 3D model of a Cheetah, along with a random amount of distractor objects, on top of a randomly chosen image. You will need to supply these images. By default the program is set to render a 2k image (that is, 2704 x 1520 pixels). Ideally all images you give to the program will thus be the same resolution or greater. Once you have found a few thousand such images, place them all in a folder called "Backgrounds" (you may have to create this folder yourself) located inside the "Cheetah" folder. The script should automatically find these images and use them at random to render images.

## 3    Usage

Once you have installed Blender, pandas, tables, and placed all the images you want in the "Backgrounds" folder, you are ready to generate some images. Run Blender, preferably by running ./blender in the terminal (whilst in the directory containing the blender executable), and open Cheetah.blend. Opening Blender through the terminal allows you to view the Python console output in the terminal window; this is recommended as you can view error messages and follow the progress of the script as it runs.

Navigate to the scripting tab of Blender if you are not already there. You should see a Python text editor, a 3D Viewport showing the Cheetah model, and an information panel. In the top right of the text editor, there is a button labelled "Run Script". You can click this when you are ready to generate images, or alternatively, press Alt+P. The only alterations you will need to make to the code are:

1. Change the containing_folder variable to the relevant absolute path to the "Cheetah" folder on your PC
2. In gen_images, ensure that the folder and rel_paths variables match, and that they show the correct output folder
3. Change the function calls to whichever of the functions are needed, ensuring that load_stuff is called first

Note that the script will overwrite any existing files with the same names once it generates new images. Ensure that if you are running the script a second time, you have renamed the existing folder, changed the folder variables, or moved the existing folder.

To generate images, simply run load_stuff() and then gen_images(1000). Replace the number 1000 with however many images you wish to render. **NOTE:** I would not recommend generating too many images at one time. If the execution fails, or some other issue interrupts the script, the annotations will not be saved correctly and you will have to start again. Unless you enjoy living life on the edge, generate a *maximum* of 1000 images at a time.
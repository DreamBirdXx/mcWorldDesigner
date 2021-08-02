mc_WorldDesigner is a level design and AI authoring tool for designing game levels, AI agents (NPCs Non player characters), for Unity game engine.
I started developing this tool for an open world RPG that I am working on, however I decided to release this for other developers to get new ideas, suggestion & to pay for my RPG development expenses. 

![alt text](https://github.com/DreamBirdXx/mcWorldDesigner/blob/main/images/main.jpg "Logo Title Text 1")

**mc_WorldDesigner has two versions (however there is not much difference).**
1. Basic is free, download it here.
2. Pro is available as subscription to partons only. Become a patreon here. (First patron tier, 3$ per month only /-)

**The system is divided into 4 components,**
1. Painter
2. Tools
3. AI
4. Settings.

all are accessiable through one editor window and merge seamlessly to provide a smooth level design experience.

Here is a brief explanation of each component, together with a tutorial to setup Mc_WorldDesigner.

## Painter.
Is the mesh painting or scattering component of mc_WorldDesigner, you can place objects manually or paint them algorithmically on any surface or unity terrain using tools such as
1. brush paint
2. area spawner and 
3. global spawner
4. Or use the path tool to, spawn objects along a spline and create fences, paths, dirt roads etc.

### Getting started with cocepts of Painter component.

**_I would highly recommend that you start a new scene and follow along the instructions in this section before you integerate the mc_WorldDesigner in your projects._**

### Setting up a test scene.
1. Create a new scene.
2. Create new new gameobject plane and scale it **x=10, y=1, z=10** and position it **x=50, y=0, z=50,** so that it's bottom  left corner is at origin.
3. mc_WorldDesigner needs to know the layer to paint on, so create a new layer name it **mc_Paint** layer. You can use any layer but for the sake of clearity we are creating a new layer. The object that you want to paint on must be set to this layer.
4. Set this new gameobject to use mc_Paint layer that we just created.
5. Open up **mc_WorldDesigner menubar-> Mc-> WorldDesigner,** you cannot init the Mc_WorldDesigner just yet.
6. Now go to **Project-> Mc_WorldDesigner-> resources** and drag mc_Renderer prefab into the scene.
7. Now go to WorldDesigner window and click init.

### Grid.
This is one of configuration steps, before you can start painting, you must have a working grid setup, the grid must cover entire dimensions of unity terrain or game object such as a plane that you want to paint on.
   Keep in mind that the origin of grid starts at origin of unity scene.

1. First go to **Mc_WorldDesigner-> Settings-> DebugSettings** and toggle on showGrid.
2. Click init grid.
3. The grid is not covering the entire dimenions of plane, so change the settings as follows to cover entire plane that we just created.
 * gridSize     -> x=100, y=100
 * worldPos     -> x=0,   y=0
 * tileDiameter -> 10

### Mc_PaintGroup.
Objects painted through are Mc_WorldEditor are classified into groups, you must have at least one active group before painting.  
   You can select, enable, disable, rename and delete individual groups.  
   You can save time by copy/ pasting settings of individual groups as well.  
   New group can be created via "G++ button" located on button panels at the bottom of the window.  

### PaintMeshes.
This is the actual mesh / game object that will be painted or scattered via any tool such as brush or area scatter tool. 
   PaintMeshes exist as assets in your project. 
   To be painted on any surface, Paint meshes are plugged into groups.  
   **Both PaintMeshes and Mc_PaintGroups have a category settings, before plugging a paint mesh into a group, make sure category of a PaintGroup and PaintMesh are same.**  

1. To create a new paint mesh go to **Project-> mc_WorldDesigner-> TestFolder-> RightClick-> Create-> mcWorldDesigner-> Painter-> PaintMesh.**
3. Paint meshes needs a game object reference and a material to be applied for referenced game object, create a new game object in scene view and drag it into **Project-> Mc_WorldDesigner-> TestFolder** change it's scale to anything you like but make sure **position and rotation is set to Vector3(0, 0, 0)**, also create a material for it.
4. Set the category of the paint mesh depending on type of gameobject you refrenced.
5. To plug a paint mesh into a group, select a group and add a new paint mesh slot click "PM++" button located on buttons panel at bottom of window.
6. Now drag the paint mesh into the new slot, and that’s it, now this mesh can be painted.
7. Select the PaintMesh by clicking the "select" button next to PaintMesh slot in editor window, selected PaintMesh's properties will appear.

### Begin scattering or painting.
Before you start painting using brush or any tool you need to tell painter the layer and tag of the object you want to paint on.
Layer is set globally for all groups while tag can set per group.

1. To set the layer go to **PainterTab-> PainterSettings-> set paint layer to mc_Paint**.
2. To set the tag go to **Group settings-> PaintOptions -> set tag to untagged** since we didn't set any tag for the plane that we created earlier.
3. Options you can ignore tags by going to **Group settings-> PaintOptions -> and toggle off useTag**

### Brush tool.

**_The easiest way to begin painting is by using brush paint tool._**
1. Enable brush by pressing "B+" button from bottom buttons panel.
2. You will see three circular radii. 
 * **Green circle** is spray radius, PaintMeshes will be spawned in this radius.
 * **Red radius** is the remove radius.
 * **Blue radius is a optional optimization, basically it halts the unnecessary behind the scale c# function calls for a particular distance radius (blue circle), since only a limited number of objects can be scattered in a spray radius (green), the distance radius stops the brush from updating hundreds of times per brush stroke to just 1 update per stroke, this gives a smooth painting experience.**.

3. Set brush settings as follows.
 * distance radius = .
 * spray radius = .
 * remove radius = .

4. To paint, hold ctrl + mouse button 1 drag to paint meshes.
5. Hold shift + mouse button 1 to remove paint. 
6. If the PaintMeshes are spawning tool close, remove them and increase distance by going to -> **Group Settings -> and change Min distance,** and then repaint.
7. After you have finished painting disable brush by going pressing "B-" located on bottom buttons panel. 


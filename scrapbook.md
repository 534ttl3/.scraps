# Panda3D tutorial 

After I'm through with the initial tutorial, and the hello world program, it's
more difficult, since now specific commands are being explained, without really
giving concrete examples to run. 


ModelNote
the GeomNodes (beneath ModelNode) contain the actual polygons

Panda has optimization mechanisms that can merge seperate Geometries together
into a mesh

egg-optchar program is designed to optimize an animated character for runtime
performance by removing unused and unneeded joints

Once you have labeled a piece of geometry, Panda's optimization mechanisms will
not fold it in to the rest of the model.

If your model is labelled (e.g. using egg-optchar), then you can find seperate, 
specific parts of the geometry using 
```
myModelsHead = myModel.find("**/theHead")
```

If I only need to scale an axis a certain way, I load a simple white square
model and set a task with model.setScale(1.00001) to scale it in time. 

In interactive mode, you can list all Sub-Nodes of a Node with
```
myNodePath.ls()
```

You can also search for NodePaths or NodePathCollections within NodePaths 
*	Matches exactly one node of any name
**	Matches any sequence of zero or more nodes
+typename	Matches any node that is or derives from the given type
-typename	Matches any node that is the given type exactly
=tag	Matches any node that has the indicated tag
=tag=value	Matches any node whose tag matches the indicated value


*instancing*:
It would seem that there must be some way avoid calculating the exact same values 50 times. There is: the technique is called instancing. The idea is this: instead of creating 50 separate dancers, create only one dancer, so that the engine only has to update her animation once. Cause the engine to render her 50 times, by inserting her into the scene graph in 50 different places. Here is how it is done:
dancer = Actor.Actor("chorus-line-dancer.egg", {"kick":"kick.egg"})
dancer.loop("kick")
dancer.setPos(0,0,0)
for i in range(50):
  placeholder = render.attachNewNode("Dancer-Placeholder")
  placeholder.setPos(i*5, 0, 0)
  dancer.instanceTo(placeholder)

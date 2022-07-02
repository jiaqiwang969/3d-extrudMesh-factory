This project is to extrude the 3D mesh from 2D polyMesh

STEP BY STEP

openfoam 7~9 env


Step1:
Create extrudeMeshDict

Then run:
```
extrudMesh 

```




Step2:
Create the createPatchDict
```
{
	// Name of new patch
	name back;

	// Type of new patch
	patchInfo
	{
		type        cyclic;
		neighbourPatch  front;
		transform translational;
		seprationVector (0 0 0.05);
	}

	constructFrom  patches;
	patches (back);
	set f0;
}
{
	// Name of new patch
	name front;

	// Type of new patch
	patchInfo
	{
		type        cyclic;
		neighbourPatch  back;
		transform translational;
		seprationVector (0 0 -0.05);
	}

	constructFrom  patches;
	patches (front);
	set f0;
}

```


Then, modify the "back" and "front" face to "cylic" in "polyMesh/boundary", 
		
```
    front
    {
        type            cyclic;
        inGroups        List<word> 1(cyclic);
        nFaces          315264;
        startFace       57515176;
        matchTolerance  0.0001;
        neighbourPatch  back;
    }
    back
    {
        type            cyclic;
        inGroups        List<word> 1(cyclic);
        nFaces          315264;
        startFace       57830440;
        matchTolerance  0.0001;
        neighbourPatch  front;
    }
```

Then, run

```
createPatch
```


[Ref](https://blog.csdn.net/jerry_cld/article/details/124264643)


Step3: 

```	
checkMesh 
```

modif 0/ to set back or front to cyclic

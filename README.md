# per-object-streamanddraw
This function enables you to set custom draw and stream distance for each object ID (or group of objects, as seen in the example).
It was created to fix disappearing objects in maps with lots of objects.
<br /><br />
Function
```c
forward CDO(modelid, Float:x, Float:y, Float:z, Float:rx, Float:ry, Float:rz);
public CDO(modelid, Float:x, Float:y, Float:z, Float:rx, Float:ry, Float:rz) 
{
    // Default values if an object is not present below
	new Float:streamingDistance = 100.0,
		Float:drawingDistance = 100.0;

	switch(modelid)
	{
		case OBJECT_ID:
			streamingDistance = 400.0,
			drawingDistance = 400.0;
	}
	return CreateDynamicObject(modelid, Float:x, Float:y, Float:z, Float:rx, Float:ry, Float:rz, .worldid = -1, .streamdistance = streamingDistance, .drawdistance = drawingDistance);
}
```
<br /><br />
Example
```c
forward CDO(modelid, Float:x, Float:y, Float:z, Float:rx, Float:ry, Float:rz);
public CDO(modelid, Float:x, Float:y, Float:z, Float:rx, Float:ry, Float:rz) 
{
	new Float:streamingDistance = 100.0,
		Float:drawingDistance = 100.0;

	switch(modelid)
	{
		// Large objects - Important, silhouettes, outer walls, big buildings, etc.
		case 4516, 4507, 18981, 19378, 19355, 19357, 18762, 19457, 19353, 19438, 3599, 19377, 11459, 18239, 16337, 19481, 16089, 694,
		17071, 19841, 17031, 19460, 19360, 19459, 19369, 19428, 19371, 19367, 19436, 19426, 9244, 11420, 1383, 2774, 1393, 8168, 19588,
		19853, 19380, 19461, 1684, 16110, 16112, 16258, 16211, 17068, 8062, 12941, 9314, 9302, 19362, 19381, 9315, 3597:
			streamingDistance = 400.0,
			drawingDistance = 400.0;

		// Medium objects - Semi-important, texts, fences, etc.
		case 1251, 1237, 981, 1423, 1459, 1282, 1424, 19087, 18980, 1256, 2942, 1257, 1483, 1342, 4642, 19327, 1408, 1506, 1557, 
		19622, 1687, 18890, 968, 3521, 16281, 8407, 1569, 2111, 8613, 7597, 1432, 8674, 672, 8397, 3861, 3243, 1570, 967, 3406,
		7914, 2722, 19943, 1532, 3034, 3926, 1499, 13025, 920, 19483, 2567, 2944, 1305, 7246, 3761, 3886, 1497, 9241, 731, 715,
		2661, 19325, 19604:
			streamingDistance = 100.0,
			drawingDistance = 100.0;

		// Small objects - Not that important, decoration, small objects you will not see from far away, etc.
		case 1238, 19419, 1425, 18652, 18647, 978, 1319, 19966, 19967, 1435, 18646, 1216, 957, 19124, 19425, 19987, 1285, 638,
		997, 9131, 2921, 18014, 1328, 3810, 644, 1294, 3460, 1372, 1343, 1478, 3802, 1265, 1415, 2840, 1450, 1364, 3801, 1985,
		1359, 637, 2245, 860, 1232, 970, 1410, 1368, 1223, 945, 2252, 15038, 632, 1214, 2048, 2801, 1728, 1670, 919, 1487, 923,
		1449, 1429, 2714, 11611, 1228, 1513, 14679, 19630, 19639, 1604, 1599, 2556, 1558, 19996, 1486, 1338, 18632, 19121, 19871,
		1453, 1280, 636, 635, 1481, 19632, 19997, 2690, 1463, 1594, 1757, 917, 2806, 1347, 1517, 19823, 11744, 19824, 1455, 1544,
		2059, 19873, 19878, 1308, 1458, 1226, 925, 1217, 851, 852, 910, 2115, 924, 3407, 933, 1431, 19831, 1462, 1448, 2945, 19927,
		1622, 1600, 1689, 3273, 640, 19975, 626, 1215, 19126, 1744, 1721, 2161, 2162, 19893, 19994, 2173, 2824, 19977, 2737, 19974,
		19989, 19894, 1318, 2854, 2284, 2271: 
			streamingDistance = 30.0,
			drawingDistance = 30.0;
	}
	return CreateDynamicObject(modelid, Float:x, Float:y, Float:z, Float:rx, Float:ry, Float:rz, .worldid = -1, .streamdistance = streamingDistance, .drawdistance = drawingDistance);
}
```
<br /><br />
How to use?
Just replace CreateDynamicObject with CDO (or whatever you called it).
```c
CreateDynamicObject(OBJECT_ID, X, Y, Z, RX, RY, RZ); 
CDO(OBJECT_ID, X, Y, Z, RX, RY, RZ); 
```

<br /><br />
For this to work, you need to use Streamer.
https://github.com/samp-incognito/samp-streamer-plugin

<br />
Before:<br />
![before](https://github.com/user-attachments/assets/65bdf38c-13a3-451a-8c03-6bb2da26c8ac)<br />
![before](https://github.com/user-attachments/assets/ededaa15-a6fa-4888-a3f4-6e052d5cc62a)
<br />
After:<br />
![after](https://github.com/user-attachments/assets/f796d5d7-382b-4aec-9a42-d57478de6218)

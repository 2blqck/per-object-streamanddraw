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
	new Float:streamingDistance = 300.0,
		Float:drawingDistance = 300.0,
		objectPriority = 1;

	switch(modelid)
	{
		case OBJECT_ID:
			streamingDistance = 400.0,
			drawingDistance = 400.0,
			objectPriority = 5;
	}
	return CreateDynamicObject(modelid, Float:x, Float:y, Float:z, Float:rx, Float:ry, Float:rz, .worldid = -1, .streamdistance = streamingDistance, .drawdistance = drawingDistance, .priority = objectPriority);
}
```
<br /><br />
Example
```c
forward CDO(modelid, Float:x, Float:y, Float:z, Float:rx, Float:ry, Float:rz);
public CDO(modelid, Float:x, Float:y, Float:z, Float:rx, Float:ry, Float:rz) 
{
	new Float:streamingDistance = 300.0,
		Float:drawingDistance = 300.0,
		objectPriority = 1;

	switch(modelid)
	{
		// Large objects - Important, silhouettes, outer walls, big buildings, etc.
		case 4516, 4507, 18981, 19378, 19355, 19357, 18762, 19457, 19353, 19438, 3599, 19377, 11459, 18239, 16337, 19481, 16089, 694,
		17071, 19841, 17031, 19460, 19360, 19459, 19369, 19428, 19371, 19367, 19436, 19426, 9244, 11420, 1383, 2774, 1393, 8168, 19588,
		19853, 19380, 19461, 1684, 16110, 16112, 16258, 16211, 17068, 8062, 12941, 9314, 9302, 19362, 19381, 9315, 3597, 9227, 19447, 3354,
		1508, 12928, 19536, 8437, 19700, 899, 659, 655, 7916, 9217, 9219, 698, 9213, 9212, 18765, 18804, 19529, 19454, 8640, 19456, 13022,
		18791, 18794, 3582, 12946, 11450, 9321, 9270, 7534, 11546, 3940, 11426, 12936, 19543, 3355, 3402, 3375, 17009, 12918, 12911, 3634,
		13367, 13369, 17324, 16406, 19463, 18827, 18763, 19441, 5726, 19455, 16776, 2669, 11694, 10166, 16134, 16133, 3556, 3252, 901, 16127,
		18807, 16010, 12943, 19532, 18800, 19629, 19533, 18805, 18777, 18999, 18830, 18770, 11423, 13607, 3330, 6295, 656, 16098, 9129, 18350,
		16302, 19550, 19649, 19002, 4106, 9125, 9128, 19531, 19445, 4842, 8253, 8038, 19464, 19465, 19856, 3279, 16327:
			streamingDistance = 405.0,
			drawingDistance = 400.0,
			objectPriority = 10;

		// Medium objects - Semi-important, texts, fences, etc.
		case 1251, 1237, 981, 1423, 1459, 1282, 1424, 19087, 18980, 1256, 2942, 1257, 1483, 1342, 4642, 19327, 1408, 1506, 1557, 
		19622, 1687, 18890, 968, 3521, 16281, 8407, 1569, 2111, 8613, 7597, 1432, 8674, 672, 8397, 3243, 3861, 967, 3406, 19604,
		7914, 2722, 19943, 1532, 3034, 3926, 1499, 13025, 920, 19483, 2567, 2944, 1305, 7246, 3761, 3886, 1497, 9241, 731, 715,
		2661, 19325, 983, 673, 19641, 1418, 669, 3594, 2789, 1597, 18648, 18766, 8657, 16003, 19439, 4227, 14395, 12921, 3374,
		3631, 12913, 1437, 3276, 19833, 708, 19482, 19863, 11714, 1649, 11495, 10757, 746, 19466, 16101, 14402, 19603, 9833, 617,
		657, 691, 684, 840, 2885, 3630, 7910, 982, 14902, 3578, 2934, 18761, 987, 7392, 14637, 16096, 11752, 1243, 1245, 3073,
		3502, 19458, 979, 14877, 14394, 3934, 10832, 1682, 14781, 14787, 16770, 3458:
			streamingDistance = 105.0,
			drawingDistance = 100.0,
			objectPriority = 5;

		// Small objects - Not that important, decoration, small objects you will not see from far away, etc.
		case 1238, 19419, 1425, 18652, 18647, 978, 1319, 19966, 19967, 1435, 18646, 1216, 957, 19124, 19425, 19987, 1285, 638,
		997, 9131, 2921, 18014, 1328, 3810, 644, 1294, 3460, 1372, 1343, 1478, 3802, 1265, 1415, 2840, 1450, 1364, 3801, 1985,
		1359, 637, 2245, 860, 1232, 970, 1410, 1368, 1223, 945, 2252, 15038, 632, 1214, 2048, 2801, 1728, 1670, 919, 1487, 923,
		1449, 1429, 2714, 11611, 1228, 1513, 19630, 19639, 1604, 1599, 2556, 1558, 19996, 1486, 1338, 18632, 19121, 19871, 996,
		1453, 1280, 636, 635, 1481, 19632, 19997, 1463, 1594, 1757, 917, 2806, 1347, 1517, 19823, 11744, 19824, 1455, 1544, 3850,
		2059, 19873, 19878, 1308, 1458, 1226, 925, 1217, 851, 852, 910, 2115, 924, 3407, 933, 1431, 19831, 1462, 1448, 2945, 19927,
		1622, 1600, 1689, 3273, 640, 19975, 626, 1215, 19126, 1744, 1721, 2161, 2162, 19893, 19994, 2173, 2824, 19977, 2737, 19974,
		19989, 19894, 1318, 2854, 2284, 2271, 1514, 14679, 19636, 19637, 19638, 2805, 19578, 1281, 1210, 2064, 2036, 849, 1345, 1710,
		2628, 2838, 2068, 1578, 1550, 2034, 2228, 2237, 2060, 1581, 1650, 1654, 18874, 2006, 19797, 19623, 19627, 737, 3516, 1231,
		19579, 3666, 1370, 1536, 3465, 2906, 2905, 2908, 11745, 11704, 18875, 19079, 14834, 19171, 19836, 17969, 18872, 1672, 2035, 
		2037, 2057, 2040, 1230, 1279, 1579, 1580, 1577, 1575, 19922, 2332, 19304, 19303, 3111, 1958, 11716, 928, 2690, 2058, 1439,
		2219, 2857, 2342, 1582, 2073, 2881, 2821, 2861, 2866, 19317, 3044, 1510, 1543, 1951, 1665, 19896, 1950, 348, 336, 335, 331,
		18673, 19169, 19812, 19924, 18633, 1574, 19926, 19923, 1496, 2204, 2907, 1771, 2047, 1271, 2357, 18066, 19792, 2804, 11735,
		2759, 11729, 1310, 3092, 19477, 19920, 19808, 19476, 1956, 1851, 2491, 2268, 1897, 2146, 14693, 19934, 19903, 19822, 18634,
		19187, 19993, 14705, 2726, 3633, 3632, 1454, 1452, 1451, 2649, 3462, 19526, 1764, 19759, 1290, 1297, 19122, 1522, 2672, 1440,
		19898, 18720, 2247, 643, 2832, 2427, 2531, 2231, 2600, 1811, 19811, 3039, 11686, 19819, 1609, 3027, 19572, 843, 845, 931, 935,
		1430, 1344, 1219, 3811, 3267, 1568, 1221, 1327, 19307, 19985, 19962, 19786, 3025, 3499, 11245, 2619, 2632, 2630, 2629, 334,
		2631, 2913, 2916, 2915, 2960, 3463, 3785, 3799, 1586, 11749, 19779, 19778, 19780, 19785, 19782, 19420, 19620, 11702, 18636,
		19773, 19942, 18637, 19784, 19781, 19783, 19515, 1242, 19142, 373, 19141, 19200, 19100, 19099, 19521: 
			streamingDistance = 35.0,
			drawingDistance = 30.0,
			objectPriority = 1;
	}
	return CreateDynamicObject(modelid, Float:x, Float:y, Float:z, Float:rx, Float:ry, Float:rz, .worldid = -1, .streamdistance = streamingDistance, .drawdistance = drawingDistance, .priority = objectPriority);
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
After:<br />
https://raw.githubusercontent.com/2blqck/per-object-streamanddraw/main/after.png<br />
<br />
Before:<br />
https://raw.githubusercontent.com/2blqck/per-object-streamanddraw/main/before-1.png<br />
https://raw.githubusercontent.com/2blqck/per-object-streamanddraw/main/before-2.png

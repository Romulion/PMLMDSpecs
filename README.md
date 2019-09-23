# PMLMDSpecs
Pokemon Masters animation file specafacation

pointer = currentglobal offset + read value  
string = int32 char count + chars  
offset - data type - description  

0   - int32 - 14  
4   - 4chars - must by "LMD0"  
24  - int32 - pointer  
28  - int32 - pointer to "format info"  
100 - float - animation duration in seconds  
104 - int32 - pointer to file name string  
116 - int32 - bones count  
120 - bones * 4 - pointers to "bone" struct  
  
"format info"  
0 - int32 - num determining format  
	==4 => +24 bytes 08 00 0C 00 04 00 08 00 08 00 00 00  
	==8 => +0 bytes  
8(+24)  - int32 - pointer to version string  
12(+24) - int32 content pointer (always 4?)  
int32 - pointer to "content name struct"  
format seems always 4 -> animation; 8 -> model  

"content name struct"  
0 - int32 - count  
4 - int32 - pointers string name  
  
"bone"  
0 - 4 bytes - entity id  
4 - int32 - pointer to name string  
8 - float - animation length in seconds  
12 - int32 - 1  
16 - int32 - 7  
20 - int32 - pointer to "anim component pointers"  
  
"anim component pointers"  
0 - 4 bytes - entity id  
4 - int32 - pointer to "unknown anim component"	has "transform struct" with unknown purpose; stride 1 element (int32 element)  
8 - int32 - pointer to "unknown anim component"	has "transform struct" with unknown purpose; stride 3 elements  
12 - int32 - pointer to rotation "transform struct" (in quaternion)  
16 - int32 - pointer to translation "transform struct"  
  
"transform struct"  
0 - 4 bytes - entity id  
4 - int32  - pointer to "time table"  
4 - int32 - 4 (pointer to element count?)  
8 - int32 - count of elements  
12 - float - element  
Rotation stored in quaternion (4 floats)  
Tralslation stored in vector3 (3 floats)  
  
"time table"  
0 - int32 - timestamp count  
4 - float - timestamp  
timestamp range from 0 to 1  

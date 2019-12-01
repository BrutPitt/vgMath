# vgMath &nbsp;v2.1
**vgMath** is a header only, compact, optimized, class math library, it contains classes to manipulate **vec**tors (with 2/3/4 components), **quat**ernions, square **mat**ricies (3x3 and 4x4).
 It contains also 4 helper functions to define Model/View/Proj matrix: **perspective**, **frustrum**, **lookAt**, **ortho**, both LeftHanded and RightHanded

Consist only of the file `vgMath.h`, plus a external `vgConfig.h` used to permit to configure it, indeed a particularity of **vgMath** is that it's configurable: it can switch from fixed type (float) for small projects or limited resources, to template classes with all types (**float** / **double** / **int** / **uint**) simply via `#define`
It uses GLSL (alias) name convention, but if is preferred, is possible to add also HLSL names type. (always via `#define`)

Other peculiarity is that it's a "subset" of [**glm** mathematics library](https://github.com/g-truc/glm), with compatible names definition, so if in a future you want pass to it, you don't need to change anything in the source code. (*HLSL types names are not compatible with **glm***)

**vgMath** is base of other my projects and tools:
- [**virtualGizmo3D**](https://github.com/BrutPitt/virtualGizmo3D) - Virtual GIZMO 3D object manipulator / orientator, via mouse, with pan and dolly/zoom features
- [**imGuIZMO.quat**](https://github.com/BrutPitt/imGuIZMO.quat) - graphic ImGui GIZMO widget a 3D object manipulator / orientator 
- [**glChAoS.P**](https://github.com/BrutPitt/glChAoS.P) 3D strange attractors GPU scout and hypercomplex fractals - over 200 Million particles in real time

**examine they to take cues: there are several example and also WebGL live demo*


## Configure vgMath
The file `vgConfig.h` allows to user to configure internal math functionality. In particular is possible select between:
 - static **float** classes (*Default*) / template classes
 - internal **vgMath** tool (*Default*) / **glm** mathematics library (it only affects [**virtualGizmo3D**](https://github.com/BrutPitt/virtualGizmo3D) / [**imGuIZMO.quat**](https://github.com/BrutPitt/imGuIZMO.quat) on which library to use internally: **vgMath** or **glm** )
 - **Right** (*Default*) / **Left** handed coordinate system (*lookAt, perspective, ortho, frustrum - functions*)
 - Add additional HLSL types name convention
 - **enable** (*Default*) / **disable** the automatic entry of `using namespace vgm;` at end of `vgMath.h`

You can do this simply by commenting / uncommenting a line in `vgConfig.h` or adding related "define" to your project, as you can see below:

```cpp
// uncomment to use TEMPLATE internal vgMath classes/types
//
// This is if you need to extend the use of different math types in your code
//      or for your purposes, there are predefined alias:
//          float  ==>  vec2 / vec3 / vec4 / quat / mat3|mat3x3 / mat4|mat4x4
//      and more TEMPLATE (only!) alias:
//          double ==> dvec2 / dvec3 / dvec4 / dquat / dmat3|dmat3x3 / dmat4|dmat4x4
//          int    ==> ivec2 / ivec3 / ivec4
//          uint   ==> uvec2 / uvec3 / uvec4
// If you select TEMPLATE classes the widget too will use internally them 
//      with single precision (float)
//
// Default ==> NO template
//------------------------------------------------------------------------------
//#define VGM_USES_TEMPLATE
```
```cpp
// uncomment to use "glm" (0.9.9 or higher) library instead of vgMath
//      Need to have "glm" installed and in your INCLUDE research compiler path
//
// vgMath is a subset of "glm" and is compatible with glm types and calls
//      change only namespace from "vgm" to "glm". It's automatically set by
//      including vGizmo.h or vgMath.h or imGuIZMOquat.h
//
// note: affects only virtualGizmo3D / imGuIZMO.quat on which library to use
//      internally: vgMath | glm
//
// Default ==> use vgMath
//      If you enable GLM use, automatically is enabled also VGM_USES_TEMPLATE
//          if you can, I recommend to use GLM
//------------------------------------------------------------------------------
//#define VGIZMO_USES_GLM
```
```cpp
// uncomment to use LeftHanded 
//
// This is used only in: lookAt / perspective / ortho / frustrum - functions
//      DX is LeftHanded, OpenGL is RightHanded
//
// Default ==> RightHanded
//------------------------------------------------------------------------------
//#define VGM_USES_LEFT_HAND_AXES
```
**From v.2.1**
```cpp
// uncomment to avoid vgMath.h add folow line code:
//      using namespace vgm | glm; // if (!VGIZMO_USES_GLM | VGIZMO_USES_GLM)
//
// Automatically "using namespace" is added to the end vgMath.h:
//      it help to maintain compatibilty between vgMath & glm declaration types,
//      but can go in confict with other pre-exist data types in your project
//
// note: this is only if you use vgMath.h in your project, for your data types:
//       it have no effect for vGizmo | imGuIZMO internal use
//
// Default ==> vgMath.h add: using namespace vgm | glm;
//------------------------------------------------------------------------------
//#define VGM_DISABLE_AUTO_NAMESPACE
```
```cpp
// uncomment to use HLSL name types (in addition!) 
//
// It add also the HLSL notation in addition to existing one:
//      alias types:
//          float  ==>  float2 / float3 / float4 / quat / float3x3 / float4x4
//      and more TEMPLATE (only!) alias:
//          double ==> double2 / double3 / double4 / dquat / double3x3 / double4x4
//          int    ==> int2 / int3 / int4
//          uint   ==> uint2 / uint3 / uint4
//
// Default ==> NO HLSL alia types defined
//------------------------------------------------------------------------------
//#define VGM_USES_HLSL_TYPES 
```
- *If your project grows you can upgrade/pass to **glm**, in any moment*
- *My [**glChAoS.P**](https://github.com/BrutPitt/glChAoS.P) project can switch from internal **vgMath** (`VGIZMO_USES_TEMPLATE`) to **glm** (`VGIZMO_USES_GLM`), and vice versa, only changing defines: you can examine it as example*




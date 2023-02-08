# MVR

Multi-View Rendering (MVR)

![](https://developer-blogs.nvidia.com/wp-content/uploads/2018/09/Multiview_CPU_GPU_Timeline.png)

## Fast Multi-View Rendering for Real-Time Applications 论文

- https://publik.tuwien.ac.at/files/publik_291961.pdf
- 论文代码：https://github.com/cg-tuwien/FastMVR

## MVR扩展

### OpenGL扩展：GL_OVR_multiview

- https://registry.khronos.org/OpenGL/extensions/OVR/OVR_multiview.txt

This extension seeks to address the inefficiency of sequential multiview rendering by adding a means to **render to multiple elements of a 2D texture array simultaneously**.  In multiview rendering, draw calls are instanced into each corresponding element of the texture array.  The vertex program **uses a new gl_ViewID_OVR variable to compute per-view values**, typically the vertex position and view-dependent variables like reflection.

### Vulkan扩展：VK_KHR_multiview 

- https://registry.khronos.org/vulkan/specs/1.3-extensions/man/html/VK_KHR_multiview.html

This extension has the same goal as the OpenGL ES **GL_OVR_multiview** extension. Multiview is a rendering technique originally designed for VR where it is more efficient to record a single set of commands to be executed with slightly different behavior for each “view”.

It includes a concise way to **declare a render pass with multiple views**, and gives implementations freedom to **render the views in the most efficient way possible**. This is done with a multiview configuration specified during render pass creation with the VkRenderPassMultiviewCreateInfo passed into VkRenderPassCreateInfo::pNext.

This extension enables the use of the SPV_KHR_multiview shader extension, which adds a new ViewIndex built-in type that allows shaders to control what to do for each view. If using GLSL there is also the GL_EXT_multiview extension that introduces a highp int gl_ViewIndex; built-in variable for vertex, tessellation, geometry, and fragment shaders.

```cpp
typedef struct VkPhysicalDeviceMultiviewProperties {
    VkStructureType    sType;
    void*              pNext;
    uint32_t           maxMultiviewViewCount;
    uint32_t           maxMultiviewInstanceIndex;
} VkPhysicalDeviceMultiviewProperties;

// NVIDIA GeForce RTX 3070
// maxMultiviewViewCount	32
// maxMultiviewInstanceIndex	134217727
```

## 驱动

## NVIDIA

- https://developer.nvidia.com/vrworks/graphics/multiview
- https://developer.nvidia.com/blog/turing-multi-view-rendering-vrworks/

## ARM

- https://community.arm.com/arm-community-blogs/b/graphics-gaming-and-vr-blog/posts/optimizing-virtual-reality-understanding-multiview

## Sample代码

- Multiview rendering in Vulkan using VK_KHR_multiview
  - https://www.saschawillems.de/blog/2018/06/08/multiview-rendering-in-vulkan-using-vk_khr_multiview/
  - https://github.com/SaschaWillems/Vulkan/blob/master/examples/multiview/multiview.cpp




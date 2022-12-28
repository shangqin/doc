## 2021.06.21 - Temporal Anti-Aliasing(TAA) Tutorial - by Sugu Lee

- https://sugulee.wordpress.com/2021/06/21/temporal-anti-aliasingtaa-tutorial/
- Code: https://github.com/leesg213/TemporalAA

## 2020.07.28 - Temporal Anti Aliasing – Step by Step - by ziacko

- https://ziyadbarakat.wordpress.com/2020/07/28/temporal-anti-aliasing-step-by-step/
- Code: https://github.com/ziacko/Temporal-AA
- Geometry/Jitter pass
```cpp
// 1) Jitter vertex shader

float deltaWidth = 1.0 / resolution.x;
float deltaHeight = 1.0 / resolution.y;

uint index = totalFrames % numSamples;
vec2 jitter = vec2(haltonSequence[index].x * deltaWidth, haltonSequence[index].y * deltaHeight);

mat4 jitterMat = mat4( 1.0 );
if(haltonScale > 0)
{
    jitterMat[3][0] += jitter.x * deltaWidth * haltonScale;
    jitterMat[3][1] += jitter.y * deltaHeight * haltonScale;
}

gl_Position = jitterMat * projection * view * translation * position; 

outBlock.newPos = projection * view * translation * position;
outBlock.prePos = projection * previousView * previousTranslation * position; 

// 2) Velocity fragment shader
// move this to UV space
vec2 newPos = ((inBlock.newPos.xy / inBlock.newPos.w) * 0.5 + 0.5);
vec2 prePos = ((inBlock.prePos.xy / inBlock.prePos.w) * 0.5 + 0.5);

vec2 velocity = (newPos - prePos);
```

# Float-Packing-GLSL
Reminder from some dude on stackoverflow: https://stackoverflow.com/questions/48288154/pack-depth-information-in-a-rgba-texture-using-mediump-precison
```GLSL
vec2 PackDepth16( in float depth ) {
    float depthVal = depth * (256.0*256.0 - 1.0) / (256.0*256.0);
    vec3 encode = fract( depthVal * vec3(1.0, 256.0, 256.0*256.0) );
    return encode.xy - encode.yz / 256.0 + 1.0/512.0;
}

float UnpackDepth16( in vec2 pack ) {
    float depth = dot( pack, 1.0 / vec2(1.0, 256.0) );
    return depth * (256.0*256.0) / (256.0*256.0 - 1.0);
}

vec3 PackDepth24( in float depth ) {
    float depthVal = depth * (256.0*256.0*256.0 - 1.0) / (256.0*256.0*256.0);
    vec4 encode = fract( depthVal * vec4(1.0, 256.0, 256.0*256.0, 256.0*256.0*256.0) );
    return encode.xyz - encode.yzw / 256.0 + 1.0/512.0;
}

float UnpackDepth24( in vec3 pack ) {
    float depth = dot( pack, 1.0 / vec3(1.0, 256.0, 256.0*256.0) );
    return depth * (256.0*256.0*256.0) / (256.0*256.0*256.0 - 1.0);
}

vec4 PackDepth32( in float depth ) {
    depth *= (256.0*256.0*256.0 - 1.0) / (256.0*256.0*256.0);
    vec4 encode = fract( depth * vec4(1.0, 256.0, 256.0*256.0, 256.0*256.0*256.0) );
    return vec4( encode.xyz - encode.yzw / 256.0, encode.w ) + 1.0/512.0;
}

float UnpackDepth32( in vec4 pack ) {
    float depth = dot( pack, 1.0 / vec4(1.0, 256.0, 256.0*256.0, 256.0*256.0*256.0) );
    return depth * (256.0*256.0*256.0) / (256.0*256.0*256.0 - 1.0);
}
```

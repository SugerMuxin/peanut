---
title: UnityShadow.md
comments: true
published: true
tags: learn

---

### Unity Shadow Solution

``` bash
$ 因为实时的阴影特别的消耗，所以在采用一种替代的实时方案。
```

原理是将Mesh的Y轴压低为0(可能在不同的建模软件导出出来的轴向的差异，这个有可能是Z轴压低为0),有时候因为美术建模的原因还需要添加一个偏移量。
然后x和z轴的长度需要根据距离来比例化Z轴。
新建一个unlit的着色器,然后添加一个_Offset偏移

```text
        
    Properties
    {
        ...
        _Offset("Offset",float) = 0
    }
        
        float _Offset;
        v2f vert (appdata v)
        {
            v2f o;
            float temp = _Offset + v.vertex.z;
            v.vertex.x +=  temp;
            v.vertex.y +=  temp;
            v.vertex.z = -_Offset;
            o.vertex = UnityObjectToClipPos(v.vertex) ;
            o.uv = TRANSFORM_TEX(v.uv, _MainTex);
            UNITY_TRANSFER_FOG(o,o.vertex);
            return o;
        }
```

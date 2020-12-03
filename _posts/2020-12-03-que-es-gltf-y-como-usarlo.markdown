---
title: "¿Qué es glTF y cómo usarlo?"
date: 2020-12-03 05:36:00 Z
published: false
---

glTF es en 3D un formato llamado GL Transmission Format, y sirve nada más y nada menos que para representar modelos en tercera dimensión. 


![sonic-3d.jpg](/uploads/sonic-3d.jpg)

Para usar glTF tenemos a la disposición bibliotecas de soporte para C#, C++, JavaScript, Java y media docena más de lenguajes de programación. Esto es útil saberlo ya que mientras no uses un lenguaje exótico siempre podrás tener la ventaja de utilizar el formato.

¿Por qué utilizar glTF?
Bueno, en primera porque su formato está desarrollado por el grupo Khronos, quienes se encargan de crear los fierros detrás de OpenGL. Luego además de ser de código abierto, junto con todas sus herramientas de implementación, tiene la ventaja de no ser privativo y no se limita a un solo conjunto de programas de modelado (como 3d Studio Max o similares), de hecho, puedes usar Blender para trabajar con él.

![opengl.png](/uploads/opengl.png)

No te preocupes si utilizas una implementación diferente a OpenGL para su procesamiento. De hecho, si utilizas el *horrendo y sobrevalorado* motor Unity, ya te contaré por qué Unity tiene esas características desde mi perspectiva en algún otro post. En fin, si utilizas Unity existen plugins que te permiten cargar glTF sin problema alguno. Y si utilizas MonoGame podrás utilizarlo también sin problema utilizando SharpGLTF.

En lo personal, y por qué no hablo de algo diferente a C#, bueno, pues es que en realidad hoy en día los videojuegos que se crean con lenguajes diferentes, y vaya que es monopólico, suelen ser más complicados de programar o más extensos, créeme, por experiencia te lo digo. 

![csharp.png](/uploads/csharp.png)

Otros lenguajes como Lua son predilectos para programar videojuegos, aunque no lo sepas, Lua es bastante utilizado en proyectos de código cerrado, también es bueno que le eches un vistazo a proyectos como Love2d mientras estás por allí.

glTF tiene además la ventaja de poseer transformaciones de huesos o "Skin transforms" que no son más que movimiento de los vértices generados por animaciones, también posee texturas, normales y materiales basados en PBR, súper cómodos y extremadamente lucidos en su calidad gráfica.

Si ya tienes como extraer los huesos de tus modelos 3D, será suficiente con pasárselos al vertex shader de OpenGL con algo como:

```
for (var i = 0; i < _effect.BoneTransforms.Length; i++)
{
    shaderProgram.SetUniform(_uniformInputBones[i], 
    _effect.BoneTransforms[i].ToSonicOrca());
}

```




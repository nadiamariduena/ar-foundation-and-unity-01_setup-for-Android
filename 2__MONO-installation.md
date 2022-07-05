## MONO

> MonoDevelop is the integrated development environment (IDE) supplied with Unity. An IDE combines the familiar operation of a text editor with additional features for debugging and other project management tasks.

<br>

##### Read this article to understand the mess [As a simple Unity indie dev, Mono and .NET still confuse me. Who is who ? Who does what?](https://stackoverflow.com/questions/48614657/as-a-simple-unity-indie-dev-mono-and-net-still-confuse-me-who-is-who-who-do)

> Depends on whether you wish to include say Linux in that. If you are asking if .NET was originally designed to target Linux then, no. However there is the .NET Compact Framework which allowed .NET code to run the Xbox 360 and Windows Phone.

There is now .NET Core, a free and open source framework which is designed for cross platform, specifically Windows, Mac and Linux.

<br>
<br>

### [What is Mono? Is it a compiler? A language? Or what?](https://answers.unity.com/questions/8555/what-is-mono-is-it-a-compiler-a-language-or-what.html)

> The answer is here: http://www.mono-project.com/What_is_Mono. Mono has a C# compiler, a runtime and a lot of libraries.

And this is the Unity3D page explaining how to integrate Unity with Visual C# (separated explanation for different Vsiual Studio C# editions): http://unity3d.com/support/documentation/Manual/VisualStudioIntegration.html

Also, you can learn C# from anywhere (a book, internet tutorials, etc.), but for basic Unity coding you need to know the C# basics. Then, learn the Unity API (using Unity's API and Scripting Reference) and putting this knowledge together you can get up and running with Unity scripting using C# pretty fast.

<br>
<br>

---

<br>

### [Confusing Threesome in Unity: C#, Mono, and IL2CPP](https://yadiyasheng.medium.com/confusing-threesome-in-unity-c-mono-and-il2cpp-df2a2e85949a)

- Unlike C++, the output of a C# compiler is not something that machines can understand and execute directly. Instead, C# source code gets compiled down to intermediate(IL) code which relies on the Common Language Runtime (CLR) to actually run on the target platform.

> Unfortunately, CLR was initially targeted to Windows platform only. So how does Unity manage to build our games for so many different platforms?

<br>

## Mono

Mono is an open-source implementation of Microsoft's .NET Framework. Basically, a bunch of talented engineers implemented .NET CLR in platforms other than Windows. Power of open source. How amazing is that!

<br>

### 🌈

Mono is indeed powerful, but it wasn’t a long term solution. Due to the amount of work and time required to develop, port, maintain new scripting features for so many platforms, Unity’s supported .net version was always lagged behind. **We were basically stuck on .NET 2.x for years! How do we get the latest C# goodness?!**

## IL2CPP

Mono served us well, but it was time to move forward.

🔴 **IL2CPP (Intermediate Language To C++) is the new scripting backend unity developed. Basically, Unity ditched mono and made their own toolchain that will transpile IL code to C++ code.** And then they make use of the C++ compiler available on the target platform (MSVC on windows, Clang on OSX for example) to produce the final executable.

<br>

##### Read More here [What is Mono? Is it a compiler? A language? Or what? / article by: Yadi Yasheng](https://answers.unity.com/questions/8555/what-is-mono-is-it-a-compiler-a-language-or-what.html)

<br>
<br>

## INstallation

- 1. choose what you need, since I use Ubuntu I will take that, then I will choose the version of ubuntu I have.

<br>

- paste the commands 1 by 1 in your terminal (root of your computer)

- At one point it will ask you (yes or Not) , if it doesnt ask you something is wrong, you might downloaded an incorrect version (it happen to me, then I realized my mistake and I changed the version)

#### [Download Mono / STEPS](https://www.mono-project.com/download/stable/)

<br>

- 2. Install Mono

```javascript
sudo apt install mono-devel
```

<br>

#### Verify Installation

https://www.mono-project.com/docs/getting-started/mono-basics/

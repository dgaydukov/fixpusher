# FixPusher 1.0.2

### Description
* Project is a fork from [sourcefourge FixPusher v1.0.2](https://sourceforge.net/projects/fixpusher/files/Version%201.0.2/src)

### Instruction to open project in Intellij IDE
* This is Ant project, so when you open it in IDE choose `create project from existing sources` (don't chose any of 4 available external sources like gradle/eclipse/maven)
* add ant plugin to your IDE
* right-click on `build.xml` (main file for ant building process) -> `Add as Ant Build File`
* go to `Ant` tab and click `Run` (green button)

### Changes to project build
I couldn't build initial project in Intellij, so I have to add a few changes so I can build project:
* change version to 2.0 in `build.xml`
* add launch4j.jar into project:
    * if you try to build original project, you would get `taskdef class net.sf.launch4j.ant.Launch4jTask can't be found`
    * cause there was no jar on the path `/usr/java/launch4j` 
    * go to [sourceforge](https://sourceforge.net/projects/launch4j) and download library
    * copy into project & change location for `launch4j` directory in `build.xml` file
* change destination to `output` folder in `build.xml`
* add all libraries required to build files into `lib` folder (I've downloaded them from pre-built fixpusher that I've downloaded from sourceforge)
* remove block from `build.xml` cause otherwise I'm getting `config doesn't support customProcName attribute`
```xml
<launch4j>
    <config chdir="." customProcName="true" dontWrapJar="true" headerType="gui" icon="etc/windows/f-logo.ico" outfile="${dist}/windows/fixpusher/FIX Pusher.exe">
        <classPath mainClass="net.sourceforge.fixpusher.view.FIXPusher">
            <cp>./lib/*.jar</cp>
        </classPath>
        <jre minVersion="1.6.0" initialHeapSize="512" maxHeapSize="512">
             <opt>-XX:MaxPermSize=256m</opt>
        </jre>
    </config>
</launch4j>
```
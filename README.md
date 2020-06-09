# PublishToMavenCentral

•	While publishing the artifacts to Maven central, it is advised to sign them to ensure it is not hampered.

•	Install GPG – GnuPG If doesn’t exists
    o	Check version in command line or GitBash
    o	gpg --version
    
•	Generate gpg key
    o	gpg --gen-key #use defaults with 4096 as key size
    o	gpg --list-secret-keys --keyid-format LONG
    o	gpg --armor --export %the key from above%

•	Update Maven settings.xml with keyname generated and passphrase used while creating.

<settings>
	……
    <profiles>  
        ……
     <profile>
         <id>ossrh</id>
         <activation>
             <activeByDefault>true</activeByDefault>
         </activation>
         <properties>
             <gpg.executable>gpg</gpg.executable>
			 <gpg.keyname>key</gpg.keyname>
             <gpg.passphrase>MySecretPassphrase</gpg.passphrase>
         </properties>
     </profile>
        ……
    </profiles>
    ……
</settings>


•	If BOM is being published, In pom.xml, set <packaging>pom</packaging>


•	Run following commands

    mvn release:prepare -P ossrh
    mvn release:perform -P ossrh
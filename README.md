<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <!-- ====================================== -->
    <!-- Project Details -->
    <!-- ====================================== -->

    <groupId>com.pos</groupId>
    <artifactId>pos-app</artifactId>
    <version>1.0</version>
    <packaging>war</packaging>

    <name>PointOfSaleApplication</name>

    <!-- ====================================== -->
    <!-- Properties -->
    <!-- ====================================== -->

    <properties>

        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>

        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>

        <junit.version>5.10.0</junit.version>

    </properties>

    <!-- ====================================== -->
    <!-- Dependencies -->
    <!-- ====================================== -->

    <dependencies>

        <!-- Servlet API -->
        <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

        <dependency>
            <groupId>jakarta.servlet</groupId>
            <artifactId>jakarta.servlet-api</artifactId>
            <version>6.0.0</version>
            <scope>provided</scope>
        </dependency>

        <!-- JUnit -->

        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>${junit.version}</version>
            <scope>test</scope>
        </dependency>

    </dependencies>

    <!-- ====================================== -->
    <!-- Build Plugins -->
    <!-- ====================================== -->

    <build>

        <finalName>pos-app</finalName>

        <plugins>

            <!-- Maven Compiler Plugin -->

            <plugin>

                <groupId>org.apache.maven.plugins</groupId>

                <artifactId>maven-compiler-plugin</artifactId>

                <version>3.11.0</version>

                <configuration>

                    <source>17</source>

                    <target>17</target>

                </configuration>

            </plugin>

            <!-- Maven WAR Plugin -->

            <plugin>

                <groupId>org.apache.maven.plugins</groupId>

                <artifactId>maven-war-plugin</artifactId>

                <version>3.4.0</version>

            </plugin>

            <!-- Surefire Plugin -->

            <plugin>

                <groupId>org.apache.maven.plugins</groupId>

                <artifactId>maven-surefire-plugin</artifactId>

                <version>3.2.5</version>

            </plugin>

            <!-- SonarQube Plugin -->

            <plugin>

                <groupId>org.sonarsource.scanner.maven</groupId>

                <artifactId>sonar-maven-plugin</artifactId>

                <version>3.10.0.2594</version>

            </plugin>
stage('Deploy to Tomcat Server') {
    sh """
    scp target/*.war ec2-user@172.31.9.72:/tmp/

    ssh ec2-user@172.31.9.72 '
        sudo cp /tmp/*.war /opt/tomcat/webapps/pos.war &&
        sudo /opt/tomcat/bin/shutdown.sh &&
        sudo /opt/tomcat/bin/startup.sh
    '
    """
}
        </plugins>

    </build>

</project># POS
Creating a portal

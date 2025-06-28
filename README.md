<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Secure Packages with CodeArtifact

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-codeartifact-updated)

**Author:** Vijay Pratap Singh Hada  
**Email:** vijaypratapsinghhada9@gmail.com

---

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-devops-codeartifact-updated_1d79e699)

---

## Introducing Today's Project!

In this project, I will demonstrate how to set up and use AWS CodeArtifact to manage and secure Java dependencies for my applications. I'm doing this project to learn how to create a reliable environment for my web app by using packages created by other developers. By storing these packages in CodeArtifact, I can ensure that my team uses the same versions, which minimizes errors and security issues. Throughout this project, I will set up an artifact repository, adjust permissions, and upload my own packages, making my development process smoother and more efficient.

### Key tools and concepts

Services I used were AWS CodeArtifact and AWS CLI. Key concepts I learned include managing package versions, creating custom packages, and verifying package integrity using security hashes. This project helped me understand how to publish and retrieve packages securely.

### Project reflection

This project took me approximately three hours to complete.



This project is part three of a series of DevOps projects where I'm building a CI/CD pipeline! I'll be working on the next project soon to continue my learning journey.



---

## CodeArtifact Repository

CodeArtifact is a secure and central place to store all your software packages. Engineering teams use artifact repositories because they provide a consistent and reliable way to manage packages and dependencies needed for building applications. With CodeArtifact, teams benefit from enhanced security by retrieving packages from a trusted source instead of risky websites. It also ensures reliability, as it serves as a backup if public package sites go down. Additionally, CodeArtifact allows teams to control which versions of packages are used, making collaboration smoother and reducing potential errors.

A domain is a way to organize multiple repositories within CodeArtifact, making it easier to manage them all together. My domain is named "nextwork," and it allows me to apply the same security and permission settings to all the repositories inside it. This is helpful because, instead of setting permissions for each repository individually, I can manage everything from one central location. 

A CodeArtifact repository can have an upstream repository, which means it can access additional libraries or packages from other sources when needed. My repository's upstream repository is Maven Central, a popular public repository for Java libraries. This connection allows my CodeArtifact repository to quickly find and store packages that may not be available locally. By using Maven Central as an upstream source, I benefit from faster access to packages, increased reliability if Maven Central is unavailable, and better control over which packages are used in my projects.

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-devops-codeartifact-updated_n4o5p6q7)

---

## CodeArtifact Security

### Issue

To access CodeArtifact, we need an authorization token that acts like a temporary password for our terminal. This token allows Maven to securely connect and fetch packages from the CodeArtifact repository. I ran into an error when retrieving a token because my EC2 instance didn't have permission to access the necessary AWS services. This happens because AWS follows the principle of least privilege, which means resources are only given the minimum permissions required to operate. 

### Resolution

To resolve the error with my security token, I made sure that my EC2 instance had the correct IAM role attached and waited a few minutes for the permissions to propagate. This resolved the error because IAM roles can take a little time to activate, and once they do, the instance can use the temporary credentials to access CodeArtifact. I also double-checked the permissions in my IAM policy to ensure they were set correctly.

It's considered a security best practice to use IAM roles because they help manage permissions without hardcoding sensitive credentials directly into applications or services. Roles allow AWS resources to assume permissions on a temporary basis, which reduces the risk of unauthorized access. By attaching specific policies to roles, you can easily control and restrict what actions can be performed, making it easier to follow the principle of least privilege.

---

## The JSON policy attached to my role

The JSON policy I set up grants permissions to access CodeArtifact by allowing actions such as getting authorization tokens, finding repository endpoints, and reading packages from the repositories. These permissions are necessary because they enable our EC2 instance to communicate with CodeArtifact securely. By allowing these specific actions, we ensure that Maven can successfully connect to the repository and manage the Java packages needed for our project. 

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-devops-codeartifact-updated_23rp7q8r9)

---

## Maven and CodeArtifact

### To test the connection between Maven and CodeArtifact, I compiled my web app using settings.xml

The settings.xml file configures Maven to connect seamlessly with CodeArtifact by storing important details like repository URLs and authentication information. It tells Maven where to find the necessary dependencies for my project and how to access the CodeArtifact repository securely. By adding the server, profile, and mirror settings to this file, I ensure that Maven knows to look for packages in CodeArtifact first and can authenticate itself automatically. 

Compiling means translating your project’s code into a format that computers can understand and run. It checks that everything is set up correctly and prepares your application to work as intended. When you compile, you're making sure that all the parts of your code come together smoothly, turning them into a functioning app

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-devops-codeartifact-updated_c17eace8)

---

## Verify Connection

After compiling, I checked my CodeArtifact repository. I noticed a list of Maven packages that had been downloaded and stored there. This showed that the system was working properly, and the dependencies I needed for my web app were now available in my repository. It was reassuring to see that the packages were fetched from Maven Central and saved for future use.

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-devops-codeartifact-updated_1d79e699)

---

## Uploading My Own Packages

In a project extension, I also decided to become a package publisher by creating and publishing my own custom package to CodeArtifact. This is useful in situations where companies need to share proprietary code internally, allowing them to manage their libraries without exposing sensitive information. 

To create my own package, I first used the CloudShell terminal to create a text file with a message. Then, I bundled this file into a tar.gz package for easy storage and transfer. I also generated a security hash because it helps ensure the package's integrity by verifying that the file hasn’t been corrupted or altered during transfer. This hash acts as a digital fingerprint, confirming that the package is secure before it's uploaded to CodeArtifact.

To publish the package, I ran the AWS CLI command to upload my tar.gz file to CodeArtifact. When I look at the package details in CodeArtifact, I can see important information such as the publication date, version number, and the origin of the package. It also shows the security hashes that confirm the package’s integrity, ensuring that my upload was successful and that the package is safe to use. 

To validate my packages, I then extracted the contents of the package. I saw my original secret message, confirming that the download was successful and the package was intact.

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-devops-codeartifact-updated_sm12-upload)

---

---

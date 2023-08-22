---
title: "Jenkins Agents: A Comprehensive Guide to Scaling Your Jenkins Environment"
seoTitle: "Jenkins Agents: A Comprehensive Guide to Scaling Your Jenkins Environm"
seoDescription: "By using Jenkins agents, you can scale up your Jenkins environment and distribute workloads across multiple machines. This allows you to run more builds"
datePublished: Fri Apr 28 2023 12:44:26 GMT+0000 (Coordinated Universal Time)
cuid: clh0jpvu8000009l58b3ldb3o
slug: jenkins-agents-a-comprehensive-guide-to-scaling-your-jenkins-environment
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682664710627/b667baf0-e241-4d84-81fd-d4667c93f1c2.png
tags: linux, devops, jenkins, 90daysofdevops, trainwithshubham

---

Jenkins is a popular automation server that is widely used in software development teams to automate the building, testing, and deployment of software. It offers a flexible and customizable platform that can be extended with a vast library of plugins. However, as your team grows and the number of projects increases, it can become challenging to manage all the workload on a single Jenkins server. This is where Jenkins agents come in.

# What are Jenkins Agents?

Jenkins agents, also known as slaves, are separate nodes that connect to the Jenkins master and handle the execution of jobs. They can be physical machines, virtual machines, or containers. Each agent is assigned a unique label that identifies it.

When you create a Jenkins job, you can specify the agent on which the job should run. When you trigger the job, the Jenkins master schedules the job to run on the specified agent. The agent then runs the job and sends the results back to the Jenkins master.

# Why Use Jenkins Agents?

By using Jenkins agents, you can scale up your Jenkins environment and distribute workloads across multiple machines. This allows you to run more builds simultaneously, reduce build times, and improve overall efficiency.

For example, suppose you have a large project with multiple components that require different environments for building and testing. In that case, you can set up multiple agents, each with a specific environment, to handle the build and test process for each component.

Another advantage of using Jenkins agents is that you can choose the type of machine or container that best suits your needs. For example, you can use a high-performance machine for CPU-intensive builds or a container for lightweight builds. This allows you to optimize your Jenkins environment for your specific requirements.

# Setting Up a Jenkins Agent

To set up a Jenkins agent, you need to install the Jenkins agent software on the machine or container you want to use as an agent. Once installed, you can configure the agent to connect to the Jenkins master using a unique secret key. You can then assign the agent to specific jobs in your Jenkins environment using the label you created for it.

Jenkins supports several methods for setting up agents, including:

* Launch agents via Java Web Start: This method allows you to launch agents on-demand from the Jenkins master using Java Web Start.
    
* Launch agents via SSH: This method allows you to launch agents on remote machines using SSH.
    
* Launch agents via JNLP: This method allows you to launch agents on remote machines using the Java Network Launching Protocol.
    

Adding and Removing Agents

One of the benefits of using Jenkins agents is that you can easily add or remove agents as your needs change. This provides a flexible and scalable solution for managing your Jenkins environment.

To add a new agent, you need to install the agent software on the machine or container and configure it to connect to the Jenkins master. Once connected, you can assign the agent to specific jobs using the label you created for it.

To remove an agent, you simply need to disconnect it from the Jenkins master. Any running jobs will be stopped, and the agent will be removed from the list of available agents.

# Conclusion

In conclusion, Jenkins agents are a powerful tool for scaling up your Jenkins environment. By distributing workloads across multiple machines, you can increase efficiency and reduce build times. If you're using Jenkins and haven't explored the use of agents yet, it's definitely worth considering as your team and workload grow.

Jenkins offers a flexible and customizable platform for building, testing, and deploying software. By using Jenkins agents, you can scale up your Jenkins environment and distribute workloads across multiple machines. This allows you to run more builds simultaneously, reduce build times, and improve overall efficiency.

Setting up Jenkins agents is relatively easy, and Jenkins provides several methods for doing so. You can also easily add or remove agents as your needs change, providing a scalable solution for managing your Jenkins environment.

One thing to keep in mind when using Jenkins agents is security. Agents can potentially have access to sensitive data and resources, so it's important to ensure that proper security measures are in place. This includes restricting access to agents based on user roles and permissions and ensuring that agents are running in secure environments.

In addition to security, it's also important to monitor and manage your Jenkins agents. This includes regularly checking the status of agents and ensuring that they are running the latest software updates and patches.

Overall, Jenkins agents are a valuable tool for managing and scaling your Jenkins environment. By distributing workloads across multiple machines, you can increase efficiency, reduce build times, and improve overall productivity. If you're using Jenkins, it's worth exploring the use of agents to see how they can benefit your team and your workflow.

### Task 1. Create an agent by setting up a node on Jenkins. Create a new AWS EC2 Instance and connect it to the master(Where Jenkins is installed). The connection of master and agent requires SSH and the public-private key pair exchange. Verify its status under the "Nodes" section.

1. Log in to your AWS console and go to the EC2 dashboard.
    
2. Launch two instances one for the master (jenkins-master) and the other as (jenkins-agent)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682672079739/ba6c2720-9bee-46d9-80f0-746ab6f59b9b.png align="center")
    
3. Install java and Jenkins on jenkins-master and configure port 8080 as we have done so many times in our previous blogs
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682672168796/90581390-bc0b-4587-a1f6-0192935dfb6b.png align="center")
    
4. Log in to the Jenkins master machine and generate a new SSH key pair using the command "ssh-keygen" in the .ssh/ folder.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682672513242/70fb3f38-10b2-489b-834d-a4df332f8b1a.png align="center")
    
5. Copy the public key from the Jenkins master machine using the command "cat ~/.ssh/id\_rsa.pub".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682672745270/8e3b7f9d-3b01-4556-ae9d-b7cec7d7485a.png align="center")
    
6. Log in to the Jenkins agent machine using SSH and add the Jenkins master public key to the authorized\_keys file using the command "vim~/.ssh/authorized\_keys" and paste the copied public key.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682673167849/bcafd8d2-357c-4623-8d30-d1dc627de8fe.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682673098844/579342e6-4fed-41fd-961c-9b5851afcf3e.png align="center")
    
7. Save and exit the file.
    
8. now by doing ssh ubuntu@&lt;jenkins\_agent&gt;
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682673435925/9b5307b5-9151-4d46-af23-91d68f9e3d9b.png align="center")
    
9. Exit from agent you can see change in ip adress below 🧐🧐🧐🧐🧐🧐🤓🥳
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682673521340/2f181341-43c1-423d-94bf-319e0009ec10.png align="center")
    
10. We have succesfully connected Master with an agent
    
11. Now lets do same using jenkins. So login to your Jenkins and click on " setup an agent"
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682673918374/a6625d67-7150-41ee-9b94-4fe6ba4ce82e.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682674034444/54abffe6-fc2b-4bbb-9f91-95cf646517b6.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682674137444/fbc93a4f-a40e-4d23-baa5-4e3d76fd10e5.png align="center")
    
12. now add credentials jenkins and paste private key from master id\_rsa into those credentials
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682674589892/5f8e365e-850d-441b-a2a4-0a9ec22949b5.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682674489616/2d1108af-ca89-48c3-ac52-259caa93eb73.png align="center")
    
13. Save and refresh
    
14. Oopsss 😣😣😣😣😣😣😣😣😣😣throwing errors but why
    
15. Ohh Java is not installed on Agent
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682675104926/a9128408-22c1-47e7-ab24-e2bdabba3e56.png align="center")
    
16. So install java
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682676055473/97a1d2fa-2f42-48bc-ab0f-8847b6c7295a.png align="center")
    
17. Lauch the node again
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682747258387/f7b9cdbd-c940-431f-98f0-4ff9b4d8af62.png align="center")
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682747512622/a14184c1-8545-4197-a202-bca2813a955b.png align="center")

😎😎😎✨✨✨🎉🎉🎉🎉 ***dev-agent in sync*** 😎😎😎✨✨✨🎉🎉🎉🎉

# Task 2: let's Assign Task to our Agent

1. Create a job pipeline of our node-todo App
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682747959930/59f138f8-380c-495d-b518-eb15636b752e.png align="center")
    
2. configure your pipeline
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682748207777/e4ef972f-3293-488a-ae2e-847b093080a7.png align="center")
    
3. Add pipeline and save
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682751290073/171e1337-ef61-40a7-ae58-8a5e007879e5.png align="center")
    
4. Expose port 8080 and add webhook on GitHub to connect GitHub with Jenkins( you can check my previous blogs on Jenkins)
    
5. Also Expose port 8000 on the agent and open the application on your browser
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682751233314/0a765680-e006-4114-a899-cc001149ec5c.png align="center")
    
6. Now click on build now
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682749403747/2879f0c1-d2a5-4e85-add4-8ffb8c7adcc1.png align="center")
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682749563729/2c4b3c50-1720-41df-95f7-cb581da5a1f8.png align="center")

As you can see :

😎😎😎✨✨✨🎉🎉🎉🎉***running on dev-agen***t 😎😎😎✨✨✨🎉🎉🎉🎉

That's it! We have successfully set up a Jenkins agent on an EC2 instance and connected it to the Jenkins master.
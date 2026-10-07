# 1.2 Attaching tools and knowledge sources

The agent exists, but it cannot yet read a document. In this task you give it the tools to do so, shape the experience a business user sees, and then run a real contract through it.

Tools are what let an agent act rather than just talk. To read an uploaded contract, this agent needs the document toolkits.

## Step 1 - Enable file uploads

First, let the agent accept a document. On the Overview tab, make sure "Allow File Uploads" is enabled. 

If its not enabled, 

(A) click the check box to enable 

(B) click Save Changes

 set Allow File Uploads to enabled and click Save Changes. Without this the agent has no way to receive the contract.

![Enable-File-Upload-Image](images/enable-fiile-upload.png)


## Step 2 -	Knowledge Source Update

This step is only to know how to update knowledge source but is not needed for this lab

In the left rail of the agent, under BUILD, 

(A) click Knowledge and review the Knowledge Sources panel. 

(B) Click Add New Source to see the source types available — Website, Document and Custom Data.

![Knowledge-Source](images/knowledge_source.png)

> Close the "Add New Knowledge Source" dialog box. This is just to know how to add new knowledge to the system

## Step 3 - Attach Tools

(A) Click Tools in the left rail. 

(B) Scroll to System Tools — these are the toolkits agentOS provides out of the box.

Select Word, PDF, Document Parser. 

> You need to scroll inside the System Tools to find Document Parser 

(C) Click Save Changes. A confirmation message appears when the agent has been updated.


![Tools-Image](images/system_tools.png)

> Why these tools? The sample contract is a Word document. Without a toolkit that can open it, the agent has nothing to analyse. Adding the PDF toolkit means the same agent also handles PDF contracts without further configuration.


## ✅ Checkpoint

- [ ] Attached Tools
- [ ] Save Changes

---

*Next: [1.3 Configuring CLI Tools →](03-conversation-conf.md)*

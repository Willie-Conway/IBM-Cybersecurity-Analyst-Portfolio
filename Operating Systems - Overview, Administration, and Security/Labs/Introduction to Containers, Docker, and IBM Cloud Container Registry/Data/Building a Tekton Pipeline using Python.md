![alt text](../Screenshots/tekton.png)

# Hands-on Lab: Building a Tekton Pipeline using Python

**Estimated time needed:** 40 minutes

Welcome to the hands-on lab for Building a Tekton Pipeline. In this lab, you will create a simple Tekton pipeline with one task in Step 1 and then add a parameter to it in Step 4. You will learn best practices for structuring a Tekton pipeline project and how to author Tekton pipelines and tasks so that they are easy to use and parameterize. You will see that Tekton allows you to reuse your pipeline-as-code artifacts, and you will look at practical approaches to publishing your pipeline and task definitions to a Git repository.

---

## Learning Objectives

After completing this lab, you will be able to:

- Create a base pipeline and task to echo a message
- Apply parameters to the task and pipeline
- Apply additional parameters to a pipeline to clone a Git repository

---

## Prerequisites

You will need the following to complete the exercises in this lab:

- A basic understanding of YAML
- A GitHub account
- An intermediate-level knowledge of CLIs

---

## Set Up the Lab Environment

You have a little preparation to do before you can start the lab.

### Step 1: Open a Terminal

Open a terminal window by using the menu in the editor: **Terminal → New Terminal**

![Terminal menu with New Terminal option highlighted]

![alt text](<../Screenshots/Terminal menu with New Terminal option highlighted.jpg>)

In the terminal, if you are not already in the `/home/project` folder, change to your project folder now:

```bash
cd /home/project
```

### Step 2: Clone the Code Repository

Now, get the code that you need to test. Use the `git clone` command to clone the Git repository:

```bash
git clone https://github.com/ibm-developer-skills-network/wtecc-CICD_PracticeCode.git
```

Your output should look similar to the image below:

![git clone command output showing repository download]

![alt text](<../Screenshots/git clone command output showing repository download.png>)

### Step 3: Change to the Labs Directory

Once you have cloned the repository, change to the labs directory:

```bash
cd wtecc-CICD_PracticeCode/labs/01_base_pipeline/
```

### Step 4: Navigate to the Labs Folder

Navigate to the `labs/01_base_pipeline` folder in the left explorer panel. All of your work will be completed with the files in this folder.

![Explorer panel showing 01_base_pipeline folder]

![alt text](<../Screenshots/Explorer panel showing 01_base_pipeline folder.png>)

### Step 5: Optional - Shorten the Command Prompt

If working in the terminal becomes difficult because the command prompt is very long, you can shorten the prompt using the following command:

```bash
export PS1="[\[\033[01;32m\]\u\[\033[00m\]: \[\033[01;34m\]\W\[\033[00m\]]\$ "
```

This will make your prompt look like:

```
[username: directory]$
```

![alt text](<../Screenshots/Optional - Shorten the Command Prompt.png>)

---

## Understanding Tekton Concepts

Before we begin building, let's understand the key Tekton concepts:

| Concept               | Description                                                                                                      |
| :-------------------- | :--------------------------------------------------------------------------------------------------------------- |
| **Task**        | A reusable, reusable collection of steps that perform a specific function (like building, testing, or deploying) |
| **Pipeline**    | A collection of tasks that run in a specific order                                                               |
| **PipelineRun** | The actual execution of a pipeline with specific parameters                                                      |
| **TaskRun**     | The actual execution of a task                                                                                   |
| **Workspace**   | A shared volume that tasks can use to pass files between each other                                              |
| **Parameter**   | Input values that can be passed to tasks and pipelines                                                           |

---

## Step 1: Create an Echo Task

In true computer programming tradition, the first task you create will echo "Hello World!" to the console.

There is starter code in the `labs/01_base_pipeline` folder for a task and a pipeline. Navigate to this folder in the left explorer panel, and open the `task.yaml` file to edit it.

### Step 1.1: Open task.yaml

Open `task.yaml` in the IDE. It should look like this:

```yaml
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: echo-hello
spec:
  steps:
    - name: echo
      image: alpine:latest
      script: |
        #!/bin/sh
        echo "Hello World!"
```

![alt text](<../Screenshots/Open task.yaml.png>)

### Step 1.2: Understand the Task Structure

Let's break down what each part of this task does:

| Component         | Value                  | Description                |
| :---------------- | :--------------------- | :------------------------- |
| `apiVersion`    | `tekton.dev/v1beta1` | Tekton API version         |
| `kind`          | `Task`               | This YAML defines a Task   |
| `metadata.name` | `echo-hello`         | The name of the task       |
| `spec.steps`    | List of steps          | Each step runs a container |
| `step.name`     | `echo`               | The name of this step      |
| `step.image`    | `alpine:latest`      | The container image to use |
| `step.script`   | Shell script           | The commands to run        |

### Step 1.3: Apply the Task to Your Cluster

To make this task available, you need to apply it using `kubectl`:

```bash
kubectl apply -f tasks.yaml
```

**Expected output:**

```
task.tekton.dev/echo-hello created
```

![kubectl apply output showing task created]

### Step 1.4: Verify the Task Was Created

```bash
kubectl get tasks
```

**Expected output:**

```
NAME          AGE
echo-hello    10s
```

---

## Step 2: Create a Pipeline

Now that you have a task, you need a pipeline to run it. Open the `pipeline.yaml` file.

### Step 2.1: Open pipeline.yaml

The starter `pipeline.yaml` should look like this:

```yaml
apiVersion: tekton.dev/v1beta1
kind: Pipeline
metadata:
  name: echo-pipeline
spec:
  tasks:
    - name: echo-task
      taskRef:
        name: echo-hello
```

### Step 2.2: Understand the Pipeline Structure

| Component             | Value                  | Description                  |
| :-------------------- | :--------------------- | :--------------------------- |
| `apiVersion`        | `tekton.dev/v1beta1` | Tekton API version           |
| `kind`              | `Pipeline`           | This YAML defines a Pipeline |
| `metadata.name`     | `echo-pipeline`      | The name of the pipeline     |
| `spec.tasks`        | List of tasks          | Tasks to run in order        |
| `task.name`         | `echo-task`          | Name of this task instance   |
| `task.taskRef.name` | `echo-hello`         | Reference to the task to run |

### Step 2.3: Apply the Pipeline

```bash
kubectl apply -f pipeline.yaml
```

**Expected output:**

```
pipeline.tekton.dev/echo-pipeline created
```

### Step 2.4: Verify the Pipeline

```bash
kubectl get pipelines
```

**Expected output:**

```
NAME             AGE
echo-pipeline    10s
```

---

## Step 3: Run the Pipeline

Now that both the task and pipeline are defined, you can run the pipeline.

### Step 3.1: Create a PipelineRun

Create a file called `pipelinerun.yaml`:

```bash
cat > pipelinerun.yaml << 'EOF'
apiVersion: tekton.dev/v1beta1
kind: PipelineRun
metadata:
  name: echo-pipelinerun
spec:
  pipelineRef:
    name: echo-pipeline
EOF
```

### Step 3.2: Apply the PipelineRun

```bash
kubectl apply -f pipelinerun.yaml
```

**Expected output:**

```
pipelinerun.tekton.dev/echo-pipelinerun created
```

### Step 3.3: Check the PipelineRun Status

```bash
kubectl get pipelineruns
```

**Expected output (while running):**

```
NAME                SUCCEEDED   REASON      STARTTIME   COMPLETIONTIME
echo-pipelinerun    Unknown     Running     10s         -
```

**Expected output (when complete):**

```
NAME                SUCCEEDED   REASON      STARTTIME   COMPLETIONTIME
echo-pipelinerun    True        Succeeded   30s         5s
```

### Step 3.4: View the Logs

To see the actual output of your pipeline:

```bash
tkn pipelinerun logs echo-pipelinerun
```

**Expected output:**

```
[echo-task : echo] Hello World!
```

![tkn pipelinerun logs showing Hello World!]

---

## Step 4: Add Parameters to the Task

Now that you have a working pipeline, let's make it more flexible by adding parameters.

### Step 4.1: Modify task.yaml with Parameters

Update `task.yaml` to accept a parameter:

```yaml
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: echo-hello
spec:
  params:
    - name: message
      type: string
      description: The message to echo
      default: "Hello World!"
  steps:
    - name: echo
      image: alpine:latest
      script: |
        #!/bin/sh
        echo "$(params.message)"
```

### Step 4.2: Apply the Updated Task

```bash
kubectl apply -f task.yaml
```

**Expected output:**

```
task.tekton.dev/echo-hello configured
```

### Step 4.3: Update pipeline.yaml with Parameters

Update `pipeline.yaml` to pass parameters to the task:

```yaml
apiVersion: tekton.dev/v1beta1
kind: Pipeline
metadata:
  name: echo-pipeline
spec:
  params:
    - name: message
      type: string
      description: The message to echo
      default: "Hello from Pipeline!"
  tasks:
    - name: echo-task
      taskRef:
        name: echo-hello
      params:
        - name: message
          value: $(params.message)
```

### Step 4.4: Apply the Updated Pipeline

```bash
kubectl apply -f pipeline.yaml
```

**Expected output:**

```
pipeline.tekton.dev/echo-pipeline configured
```

### Step 4.5: Run with Default Parameter

Create a new PipelineRun:

```bash
cat > pipelinerun-default.yaml << 'EOF'
apiVersion: tekton.dev/v1beta1
kind: PipelineRun
metadata:
  name: echo-pipelinerun-default
spec:
  pipelineRef:
    name: echo-pipeline
EOF

kubectl apply -f pipelinerun-default.yaml
```

### Step 4.6: View the Logs

```bash
tkn pipelinerun logs echo-pipelinerun-default
```

**Expected output:**

```
[echo-task : echo] Hello from Pipeline!
```

### Step 4.7: Run with Custom Parameter

Create a PipelineRun with a custom message:

```bash
cat > pipelinerun-custom.yaml << 'EOF'
apiVersion: tekton.dev/v1beta1
kind: PipelineRun
metadata:
  name: echo-pipelinerun-custom
spec:
  pipelineRef:
    name: echo-pipeline
  params:
    - name: message
      value: "Welcome to Tekton!"
EOF

kubectl apply -f pipelinerun-custom.yaml
```

### Step 4.8: View the Custom Logs

```bash
tkn pipelinerun logs echo-pipelinerun-custom
```

**Expected output:**

```
[echo-task : echo] Welcome to Tekton!
```

---

## Step 5: Create a Git Clone Task

Now let's create a more practical task that clones a Git repository.

### Step 5.1: Create a New Task File

Create `git-clone-task.yaml`:

```yaml
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: git-clone
spec:
  params:
    - name: url
      type: string
      description: The Git repository URL to clone
    - name: revision
      type: string
      description: The revision to checkout (branch, tag, or commit)
      default: "main"
  workspaces:
    - name: source
      description: The workspace to clone the repository into
  steps:
    - name: clone
      image: alpine/git:latest
      script: |
        #!/bin/sh
        cd $(workspaces.source.path)
        echo "Cloning repository: $(params.url)"
        git clone --depth 1 --branch $(params.revision) $(params.url) repo
        cd repo
        echo "Clone successful! Contents:"
        ls -la
```

### Step 5.2: Apply the Git Clone Task

```bash
kubectl apply -f git-clone-task.yaml
```

**Expected output:**

```
task.tekton.dev/git-clone created
```

---

## Step 6: Create a Pipeline with Workspace

Now create a pipeline that uses the git-clone task with a workspace.

### Step 6.1: Create the Pipeline

Create `clone-pipeline.yaml`:

```yaml
apiVersion: tekton.dev/v1beta1
kind: Pipeline
metadata:
  name: clone-pipeline
spec:
  params:
    - name: repo-url
      type: string
      description: The Git repository URL to clone
    - name: revision
      type: string
      description: The revision to checkout
      default: "main"
  workspaces:
    - name: shared-workspace
      description: The workspace to share between tasks
  tasks:
    - name: clone-repo
      taskRef:
        name: git-clone
      workspaces:
        - name: source
          workspace: shared-workspace
      params:
        - name: url
          value: $(params.repo-url)
        - name: revision
          value: $(params.revision)
```

### Step 6.2: Apply the Pipeline

```bash
kubectl apply -f clone-pipeline.yaml
```

**Expected output:**

```
pipeline.tekton.dev/clone-pipeline created
```

---

## Step 7: Run the Clone Pipeline

### Step 7.1: Create a PipelineRun with Workspace

Create `clone-pipelinerun.yaml`:

```yaml
apiVersion: tekton.dev/v1beta1
kind: PipelineRun
metadata:
  name: clone-pipelinerun
spec:
  pipelineRef:
    name: clone-pipeline
  params:
    - name: repo-url
      value: "https://github.com/ibm-developer-skills-network/wtecc-CICD_PracticeCode.git"
    - name: revision
      value: "main"
  workspaces:
    - name: shared-workspace
      volumeClaimTemplate:
        spec:
          accessModes:
            - ReadWriteOnce
          resources:
            requests:
              storage: 1Gi
```

### Step 7.2: Apply the PipelineRun

```bash
kubectl apply -f clone-pipelinerun.yaml
```

### Step 7.3: Check the Status

```bash
kubectl get pipelineruns
```

### Step 7.4: View the Logs

```bash
tkn pipelinerun logs clone-pipelinerun
```

**Expected output:**

```
[clone-repo : clone] Cloning repository: https://github.com/ibm-developer-skills-network/wtecc-CICD_PracticeCode.git
[clone-repo : clone] Cloning into 'repo'...
[clone-repo : clone] Clone successful! Contents:
[clone-repo : clone] total 12
[clone-repo : clone] drwxr-xr-x 3 root root 4096 ... labs
[clone-repo : clone] -rw-r--r-- 1 root root ... README.md
```

---

## Step 8: Create a Python Application Task

Let's create a task that runs a Python script.

### Step 8.1: Create a Python Task

Create `python-task.yaml`:

```yaml
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: run-python
spec:
  params:
    - name: script
      type: string
      description: The Python script to run
      default: |
        print("Hello from Python!")
  steps:
    - name: run-python
      image: python:3.9-slim
      script: |
        #!/bin/sh
        python -c "$(params.script)"
```

### Step 8.2: Apply the Python Task

```bash
kubectl apply -f python-task.yaml
```

### Step 8.3: Create a PipelineRun with Python Script

Create `python-pipelinerun.yaml`:

```yaml
apiVersion: tekton.dev/v1beta1
kind: PipelineRun
metadata:
  name: python-pipelinerun
spec:
  pipelineSpec:
    tasks:
      - name: run-python-task
        taskRef:
          name: run-python
        params:
          - name: script
            value: |
              import sys
              import platform
              print(f"Python version: {sys.version}")
              print(f"Platform: {platform.platform()}")
              print("Tekton pipeline executed successfully!")
```

### Step 8.4: Apply and View Logs

```bash
kubectl apply -f python-pipelinerun.yaml
tkn pipelinerun logs python-pipelinerun
```

**Expected output:**

```
[run-python-task : run-python] Python version: 3.9.18 (main, ...)
[run-python-task : run-python] Platform: Linux-...
[run-python-task : run-python] Tekton pipeline executed successfully!
```

---

## Step 9: Best Practices for Tekton Pipelines

### Step 9.1: Use Parameter Defaults

Always provide sensible defaults for parameters:

```yaml
params:
  - name: revision
    type: string
    default: "main"
    description: Git branch or tag to checkout
```

### Step 9.2: Add Descriptions

Document your tasks and parameters:

```yaml
metadata:
  name: my-task
  annotations:
    description: "This task does something important"
    version: "1.0.0"
```

### Step 9.3: Use Workspaces for Data Sharing

Always use workspaces for sharing data between tasks:

```yaml
workspaces:
  - name: source
    description: The workspace containing source code
```

### Step 9.4: Structure Your Repository

Organize your Tekton resources in a consistent directory structure:

```
tekton/
├── tasks/
│   ├── build.yaml
│   ├── test.yaml
│   └── deploy.yaml
├── pipelines/
│   └── ci-cd.yaml
└── runs/
    └── production-run.yaml
```

---

## Step 10: Clean Up Resources

### Step 10.1: List All Resources

```bash
kubectl get tasks
kubectl get pipelines
kubectl get pipelineruns
```

### Step 10.2: Delete PipelineRuns

```bash
kubectl delete pipelinerun echo-pipelinerun
kubectl delete pipelinerun echo-pipelinerun-default
kubectl delete pipelinerun echo-pipelinerun-custom
kubectl delete pipelinerun clone-pipelinerun
kubectl delete pipelinerun python-pipelinerun
```

### Step 10.3: Delete Pipelines and Tasks

```bash
kubectl delete pipeline echo-pipeline clone-pipeline
kubectl delete task echo-hello git-clone run-python
```

---

## Summary of Files Created

| File                       | Purpose                                   |
| :------------------------- | :---------------------------------------- |
| `task.yaml`              | Echo task with parameter support          |
| `pipeline.yaml`          | Pipeline that uses the echo task          |
| `pipelinerun.yaml`       | Runs the pipeline with default parameters |
| `git-clone-task.yaml`    | Task for cloning Git repositories         |
| `clone-pipeline.yaml`    | Pipeline using the git-clone task         |
| `clone-pipelinerun.yaml` | Runs the clone pipeline                   |
| `python-task.yaml`       | Task for running Python scripts           |

---

## Summary

In this hands-on lab, you have:

| Activity                                    | Completed |
| :------------------------------------------ | :-------- |
| Cloned the practice code repository         | ✓        |
| Created a basic Tekton task                 | ✓        |
| Created a Tekton pipeline                   | ✓        |
| Ran a pipeline and viewed logs              | ✓        |
| Added parameters to tasks and pipelines     | ✓        |
| Ran pipelines with custom parameters        | ✓        |
| Created a Git clone task                    | ✓        |
| Configured workspaces for data sharing      | ✓        |
| Created a Python script task                | ✓        |
| Applied best practices for Tekton resources | ✓        |
| Cleaned up resources                        | ✓        |

---

## Key Takeaways

### Tekton Resource Types

| Type                  | Purpose                          |
| :-------------------- | :------------------------------- |
| **Task**        | Reusable unit of work with steps |
| **Pipeline**    | Collection of tasks in sequence  |
| **PipelineRun** | Execution of a pipeline          |
| **TaskRun**     | Execution of a task              |
| **Workspace**   | Shared storage between tasks     |

### Parameter Types

| Type       | Description     |
| :--------- | :-------------- |
| `string` | Text value      |
| `array`  | List of strings |
| `object` | Key-value pairs |

### Best Practices

1. **Use descriptive names** for tasks, pipelines, and parameters
2. **Add documentation** using annotations and descriptions
3. **Provide default values** for parameters when possible
4. **Use workspaces** for sharing data between tasks
5. **Version your resources** with annotations
6. **Organize files** in a consistent directory structure
7. **Test locally** before deploying to production

---

## Troubleshooting Tips

| Issue                               | Solution                                                   |
| :---------------------------------- | :--------------------------------------------------------- |
| **Task not found**            | Ensure you applied the task:`kubectl apply -f task.yaml` |
| **PipelineRun stuck**         | Check status:`kubectl get pipelineruns -w`               |
| **Permission denied**         | Check workspace permissions and service accounts           |
| **Git clone fails**           | Verify repository URL and credentials                      |
| **Container image not found** | Check image name and pull policy                           |

---

## Additional Resources

- [Tekton Documentation](https://tekton.dev/docs/)
- [Tekton Pipelines GitHub](https://github.com/tektoncd/pipeline)
- [Tekton CLI (tkn) Documentation](https://github.com/tektoncd/cli)

---

## Congratulations!

You have successfully completed the **Building a Tekton Pipeline using Python** lab. You now know how to:

- Create Tekton tasks and pipelines
- Add parameters to make pipelines reusable
- Use workspaces to share data between tasks
- Create practical tasks for Git cloning and running Python scripts
- Apply best practices for Tekton pipeline development

These skills are essential for implementing CI/CD pipelines in Kubernetes environments using Tekton.

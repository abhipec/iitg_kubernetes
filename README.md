# Instructions for using IITG CSE Dept. Kubernetes cluster


## Kubernetes setup information

Information on the number of systems in the Kubernetes cluster along with the configuration is available at: [http://jatinga.iitg.ernet.in/cseintranet/compufacility](http://jatinga.iitg.ernet.in/cseintranet/compufacility) (Intranet link)

## Account creation and login details

To get an account, please contact Mr. Bhriguraj Borah, CSE Technical officer. Once the account is created, a user will get login details of a login node. The login node has Ubuntu 18.04 OS installed, with neither GPU support nor any computational tools such as TensorFlow or Pytorch installed. The user is requested to copy all the necessary code/data to the login node and submit a CPU/GPU job to kubernetes cluster using the instructions mentioned below.

## What is Docker and Kubernetes?

If there terms are new to you, please refer to these resources.


* A brief introduction of docker (video): [https://www.youtube.com/watch?v=rmf04ylI2K0](https://www.youtube.com/watch?v=rmf04ylI2K0)
* A beirf intorduction of docker (blog): [https://opensource.com/resources/what-docker](https://opensource.com/resources/what-docker)
* A brief introduction of kubernetes (video): [https://www.youtube.com/watch?v=R-3dfURb2hA](https://www.youtube.com/watch?v=R-3dfURb2hA)
* A brief introduction of kubernetes (documentation): [https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/) 


## How to submit a job request to Kubernetes cluster

### Job description file
Create a job file for the task that you need to execute on the cluster.
A sample job file is available at [https://iitgoffice-my.sharepoint.com/:w:/g/personal/abhishek_abhishek_iitg_ac_in/EQEcxggq5oRGipp_XCBGY2gBs8Vbb3KSbL7BU_bAiYRm1A?e=sAFhU6](https://iitgoffice-my.sharepoint.com/:w:/g/personal/abhishek_abhishek_iitg_ac_in/EQEcxggq5oRGipp_XCBGY2gBs8Vbb3KSbL7BU_bAiYRm1A?e=sAFhU6)


### Submitting a job request

Submit the job using the following command:
```
kubectl create -f job_description_file.yaml
```

### Monitoring job progress and debugging

#### Job status

To check the status of the job, use the following command:

```
kubectl get pods
```

The status messages have the following meaning:

| Status | Meaning |
|--------|---------|
| Running | The job is currently running. |
| CreatingContainer | The Kubernetes cluster is creating the docker container. It might take some time, especially when a new docker image is pulled from the docker hub site.|
| Error | The job terminated with an error |
| Completed | The job has successfully completed |
| Pending | The scheduler is waiting for a node which has the requested resources available. |
| ImagePullBackOff | It occurs when their is an issue in pulling the specified docker image either due to internet connectivity or wrong image name. |

#### Monitoring job

If the job in execution prints output to stdout, then to view that output, you can use the kubectl logs command mentioned below. This will continuously display the stdout messages on the terminal. Also if the job is terminated with the Error status, detailed information of the error will be provided by this command.

```
kubectl logs -k pod/name_of_the_pod_in_job_description_file
```

Also, if the job is with the running status, it is possible to attach the shell withing the container to your terminal with the following command.

```
kubectl exec -it pod_name bash
```

#### Pending jobs

To know why a job is in pending status, use the following command:
```
kubectl describe pod name_of_the_pod
```

### Dashboard

Details of all user submitted pods running on the cluster are available at: [http://172.16.117.58:5000/](http://172.16.117.58:5000/)



# **Using `emptyDir` for Scratch Space**

## Lab Overview
This lab focuses on using an `emptyDir` volume in Kubernetes to provide shared storage space between containers in the same Pod. This volume type is useful for temporary storage needs within a pod.

## Pre-requisites
- Kubernetes cluster running and kubectl configured
- Basic understanding of Pods and Volumes

## Outcomes
- Understand how to use `emptyDir` volumes in Pods
- Learn how to share data between containers in the same Pod

## Description
In this lab, we will create a Pod with two containers. One container writes data to an `emptyDir` volume, and the other container reads the data. `emptyDir` volumes are ephemeral, meaning they are destroyed when the Pod is deleted.

## TASKS

1. **Create a Pod manifest with two containers: one writes data, and the other reads it.**

   - **Command:**  
     Create a file named `pod-emptydir.yaml` with the following content:

     ```yaml
     apiVersion: v1
     kind: Pod
     metadata:
       name: test-pd
     spec:
       containers:
       - name: writer
         image: busybox
         command: ['sh', '-c', 'echo "Data from writer container" > /cache/data.txt && sleep 3600']
         volumeMounts:
         - name: cache-volume
           mountPath: /cache
       - name: reader
         image: busybox
         command: ['sh', '-c', 'cat /cache/data.txt && sleep 3600']
         volumeMounts:
         - name: cache-volume
           mountPath: /cache
       volumes:
       - name: cache-volume
         emptyDir: {}
     ```

     **Explanation:**
     - The `emptyDir` volume is defined under `volumes` and mounted to both containers under `/cache`.
     - The `writer` container writes data into the `/cache/data.txt` file, while the `reader` container is simply set up to sleep, allowing you to check the mounted data.

2. **Apply the Pod manifest using kubectl.**

   - **Command:**  
     ```bash
     kubectl apply -f pod-emptydir.yaml
     ```

     **Explanation:**
     - `kubectl apply -f pod-emptydir.yaml` creates the Pod as defined in the manifest file. It ensures both containers mount the `emptyDir` volume and allows the writer container to populate the volume with data.

3. **Check the logs of the reading container to verify it reads the data written by the first container.**

   - **Command:**  
     ```bash
     kubectl logs test-pd -c reader
     ```

     **Explanation:**
     - `kubectl logs test-pd -c reader` fetches the logs from the `reader` container in the `test-pd` pod. You should see that the `reader` container accesses the `/cache/data.txt` file, confirming that the data written by the `writer` container is available.

4. **Delete the Pod and verify that the data in the `emptyDir` volume is removed.**

   - **Command:**  
     ```bash
     kubectl delete pod test-pd
     ```

     **Explanation:**
     - `kubectl delete pod test-pd` deletes the pod, which automatically cleans up the `emptyDir` volume. You can verify the volume has been removed as it's ephemeral and does not persist after the Pod's deletion.

## Submission Guidelines
- Submit the YAML file for the Pod manifest.
- Provide the logs output from the `reader` container.

Note: The screenshots and the file content should be added to a google doc or google drive the link to which should be shared with permissions set as `accessible to all`

## Additional Resources
- [emptyDir](https://kubernetes.io/docs/concepts/storage/volumes/#emptydir)
# Application-traces-to-Grafana-Tempo-by-kustomization.yaml-file

![Screenshot 2024-11-23 163906](https://github.com/user-attachments/assets/ebebcdd5-5276-4df4-b964-3a6b45490fe0)

![Screenshot 2024-11-23 164238](https://github.com/user-attachments/assets/b00c17d1-58a6-46b4-b418-abec28e5f4f8)

These screenshot help you understand how to use kustomization.yaml to get the application traces to Grafana, It will help undersatand in which directory what files should be there.

Here in the ** dir** directory I have files for kustomization, configmap, deployment, service and also a data directory. In data directory I have my otel configuration as shown in the screenshot.

Now after making all the changes:

1. Come back to ** Dir** directory and run this command to apply the changes in dir directory

   kubectl apply -k .

   This will create the deployments, configmaps, services, and pods

3. Now run the command

  kubectl get pods - it will show all the pods

  kubectl delete pod <applicatiobn-pod-name> - this will restart the pod and refresh changes

  kubectl delete pod <otel-collector-pod> - this will restart otel- collector pod

  kubectl get pods - new pods will come

  kubectl logs <applicatiobn-pod-name> - you should see the  metrics, traces and logs

  kubectl logs <otel-collector-pod> you should see that otel is ready to get the data


3. Now Run the port-forward command as the service type for application is ClusterIP

   first run, kubectl get svc --- this will get you all the service names

   Now run kubectl port-forward svc/<service-name of application> 8000:8000

   Now curl 127.0.0.1:8000/docs to see the apllication giving the traces on console and

   go to grafana explore and see the traces coming
   


Reference links
https://github.com/open-telemetry/opentelemetry-collector/blob/main/exporter/otlphttpexporter/README.md

https://medium.com/incerto-technologies/simple-opentelemetry-setup-in-a-kubernetes-environment-aa7dc3e3fcf9



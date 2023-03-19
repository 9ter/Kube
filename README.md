
## Kubernetes In Windows

## Wakatime
https://wakatime.com/@spcn25/projects/xxjqnvkraf

## Ref
https://github.com/TanankornMoonprathom/Kube
https://github.com/KanchanaRangcharoen/Kube

## 1. Install Kubectl
   - Ref 
    - https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/

   - download Kubectl.exe to path want

      ```
      curl.exe -LO "https://dl.k8s.io/release/v1.26.0/bin/windows/amd64/kubectl.exe"
      ``` 
   - Add Path to environment variable
      - Search environment
  
        ![image](https://user-images.githubusercontent.com/119097663/224904080-a7de4fcd-c43d-4760-b483-0734aaeca796.png)


      - Click Environment Variables...

        ![image](https://user-images.githubusercontent.com/119097663/224904504-ac4bb0b8-4a35-4ddd-87c0-d0f665c86d04.png)

       - Select Path Click Edit

        ![image](https://user-images.githubusercontent.com/119097663/224904590-64c1e452-efae-41f9-861e-409f9e9b9e78.png)

       - Click New
        
        ![image](https://user-images.githubusercontent.com/119097663/224904653-d6231336-cf6a-4280-bdba-2e72043c5a5c.png)

      - Add Path that have kubectl.exe
      - Click OK
  
      - Test Kubectl enable in command
      ```ruby
      kubectl version --client
      ```

## 2. Install minikube
   - Ref
    - https://minikube.sigs.k8s.io/docs/start/

      - download minikube.exe

      ```ruby
      New-Item -Path 'c:<path want to install>' -Name 'minikube' -ItemType Directory -Force #create folder minikube
      Invoke-WebRequest -OutFile 'c:<path want to install>\minikube\minikube.exe' -Uri 'https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe' -UseBasicParsing #download install to path
      ```

      - Add Path to environment variable
      ```ruby
      $oldPath = [Environment]::GetEnvironmentVariable('Path', [EnvironmentVariableTarget]::Machine)
      if ($oldPath.Split(';') -inotcontains 'C:<path folder minikube.exe>'){ `
      [Environment]::SetEnvironmentVariable('Path', $('{0};C:<path folder minikube.exe>' -f $oldPath), [EnvironmentVariableTarget]::Machine) `
      }
      ```
   - Restart Terminal

## 3. Install Docker Desktop
   - Ref
    - https://docs.docker.com/desktop/install/windows-install/

## Test minikube start
1. Start a cluster using the docker driver
   ```ruby
   minikube start --driver=docker
   ```
   ![image](https://user-images.githubusercontent.com/98762543/226186945-0f334abf-5bab-4c3b-bd93-3395953835b8.png)

2. Run with open dashboard
   ```ruby
   minikube dashboard
   ```
   ![image](https://user-images.githubusercontent.com/98762543/226186966-06e51b81-db0f-4e26-82af-d2f4f30137d9.png)

3. Test services
   ```ruby
   minikube service hello-minikube
   ```
   ![image](https://user-images.githubusercontent.com/119097663/224907641-f32599e8-afd0-4a9e-8bf5-f8a59c476752.png)

4. Test Stop minikube
   ```ruby
   minikube pause
   ```
   ![image](https://user-images.githubusercontent.com/119097663/224907200-c1758b1c-03a8-40b2-9d5d-258644100325.png)

## 4. Install traefik
1. Install Traefik Resource Definitions
   ```ruby
   kubectl apply -f https://raw.githubusercontent.com/traefik/traefik/v2.9/docs/content/reference/dynamic-configuration/kubernetes-crd-definition-v1.yml
   ```
    ![image](https://user-images.githubusercontent.com/98762543/226187109-13febdfc-8359-4952-ad10-652f7b8addde.png)

2. Install RBAC for Traefik
   ```ruby
   kubectl apply -f https://raw.githubusercontent.com/traefik/traefik/v2.9/docs/content/reference/dynamic-configuration/kubernetes-crd-rbac.yml
   ```
    ![image](https://user-images.githubusercontent.com/98762543/226187151-438a9b42-3e2f-447d-b4f5-c097b594fbea.png) 

3. Install Traefik Helmchart
   ```ruby
   helm repo add traefik https://traefik.github.io/charts 
   helm repo update 
   helm install traefik traefik/traefik 
   ```
   ![image](https://user-images.githubusercontent.com/98762543/226187245-b86a9148-ca99-4e3e-a88f-f4d948869797.png)

4. Verify service is running
   ```ruby
   kubectl get svc -l app.kubernetes.io/name=traefik
   kubectl get po -l app.kubernetes.io/name=traefik
   ```
   

5. copy user in dashboard-secret place it at user in traefik-dashboard


6. Deploy
   ```ruby
   kubectl apply -f . 
   ```
   ![image](https://user-images.githubusercontent.com/98762543/226187372-a22e3b51-0719-4c10-b87d-029e2b4a95d9.png)

## Result

## 1. dashboard

![image](https://user-images.githubusercontent.com/98762543/226186966-06e51b81-db0f-4e26-82af-d2f4f30137d9.png)

## 2. https://traefik.spcn25.local/dashboard/#/

![image](https://user-images.githubusercontent.com/98762543/226187618-971f8f12-712b-4dad-909d-49da7e19daae.png)

## 5. http://web.spcn25.local/

![image](https://user-images.githubusercontent.com/98762543/226187632-bf6378f5-e3f9-4e23-8eb8-9964977e61a5.png)

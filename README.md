# Blueprint for the project

### What does this blueprint contains?

The necessary previous steps to start working right away.

- [ ] The docker environment running and functioning
- [ ] The backend application running and functioning
- [ ] The frontend application running and functioning
- [ ] The nginx server running and functioning
- [ ] Ansible Playbook to deploy the application to a VPS

#### Docker Environment

The application will consist of an nginx server that handles the requests of both backend and frontend applications. The backend will be a node.js application and the frontend will be a react application.

The docker-compose file will contain the following services:

- nginx
- backend
- frontend

The nginx service will be the entry point of the application, it will handle the requests and redirect them to the backend or frontend services.

The backend service will be a node.js application that will handle the requests from the frontend and interact with external services.

The frontend service will be a react application that will be served by the nginx server.

#### Ansible Playbook

The ansible playbook will contain the necessary steps to deploy the application to a VPS. The playbook will contain the following steps:

- Install docker
- Install docker-compose
- Clone the repository
- Run the docker-compose file

_Note: for ansible to work, you need to have the ssh keys configured and python installed on the VPS._

##### How ansible works?

Ansible is a tool that allows you to automate the deployment of applications to a VPS. It uses a playbook that contains the necessary steps to deploy the application.

- Controller node. The controller node is the machine that runs the ansible playbook and the managed node is the machine that will receive the commands from the controller node. In our case, the controller node on local development and testing, will be the local machine from which ansible is being executed, but for production, the controller node might be the github action pipeline.
- Managed node. The managed node is the machine that will receive the commands from the controller node. In our case, the managed node will be the VPS where the application will be deployed.
- Inventory. The inventory is a file that contains the list of managed nodes that ansible will deploy the application to. The inventory file is written in yaml and contains the list of managed nodes that ansible will deploy the application to.
- Modules. Predefined code to perform specific tasks (e.g., installing packages, managing files).
- Playbook. Define the tasks Ansible performs on managed nodes.
- Roles. A way to structure tasks, variables, files, and templates for reusability.

### How to start the environment?

To start the production environment, you need to run the following command:

```bash
docker-compose up # --build if you want to rebuild the images
```

To start the development environment, you need to run the following command:

```bash
docker-compose -f docker-compose.dev.yml up # --build if you want to rebuild the images
```

On local development, you can access the frontend application on `http://localhost:3000` and the backend application on `http://localhost:5000/api`.

### Troubleshooting when running the above commands

If you encounter any issues when running the above commands, try deleting the volumes and the images and running the commands again.

```bash
docker system prune -a --volumes -f
```

### Testing ansible on local with a VM

To test ansible on local with a VM, you need to have the following tools installed:

- VirtualBox
- Vagrant
- Ansible

After installing the tools, you need to run the following commands inside the ansible_dev directory:

```bash
vagrant up
```

This command will create a VM with the necessary tools to run ansible. After the VM is created, you can run the following command to test the ansible playbook:

```bash
ansible-playbook -i inventory.ini playbook.yml
```

Then, we can access the VM by running the following command:

```bash
vagrant ssh
```

Inside the VM, we can check that everything is running and installed as intended :)

You can check the page by running the following command:

```bash
curl http://192.168.56.101:80 # nginx
curl http://192.168.56.101:3000 # frontend
curl http://192.168.56.101:80/api # backend
```

NEED TO FIGURE OUT HOW TO INTEGRATE NGINX WITH THE FRONTEND

### Running ansible on the production Environment

Still working on this part, but the idea is to have a github action that will run the ansible playbook on the VPS. The playbook will contain the necessary steps to deploy the application to the VPS.

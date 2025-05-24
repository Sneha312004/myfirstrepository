Step 1: Launch WSL (Ubuntu) on Windows Press Windows + S, type "Ubuntu" and open it. Update the package list:sudo apt update && sudo apt upgrade -yStep 2: Install Ansible
sudo apt install ansible -y
Verify the installation:ansible --version
Step 3: Configure the Inventory FileCreate a simple inventory file (inventory.ini):mkdir ~/ansible-lab
cd ~/ansible-lab
nano inventory.ini
Add this content:[local]localhost ansible_connection=local
Step 4: Test Ansible Connectionansible -i inventory.ini all -m ping
Expected Output:localhost | SUCCESS => {"changed": false,
"ping": "pong"}Step 5: Create an Ansible Playbooknano basic-setup.ymlPlaybook Content:
- name: Basic Setup Example
- hosts: all
- become: yes
- tasks:
- - name: Install Nginx
  - apt:
  - name: nginx
  - Step 6: Run the Playbook
  - ansible-playbook -i inventory.ini basic-setup.yml
  - Observe each task being executed and check the status.
  - Step 7: Verify Nginx Installationcurl http://localhost  Expected Output: Default Nginx HTML page content.
  - state: present
  - update_cache: yes
  - - name: Ensure Nginx is running
    - service:
    - name: nginx
    - state: started
    - enabled: yes

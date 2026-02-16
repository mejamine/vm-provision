# Linux VM Provisioning Playbook

This Ansible project provisions Linux VMs using KVM/libvirt.

---

# 1️⃣ Run Locally (Classic Ansible)

```bash
ansible-playbook playbooks/main.yml --ask-become-pass
```

You will be prompted for the sudo password.

---

# 2️⃣ Run with Execution Environment (Ansible Navigator)

## Run the Playbook

```bash
ansible-navigator run main.yml \
  --eei docker.io/<dockerhub username>/kvm-libvirt-ee:1.0 \
  --execution-environment true \
  --container-engine podman \
  -i inventory/hosts.ini \
  -e @pass.yml
```

## pass.yml File

Create a file named `pass.yml`:

```yaml
ansible_become_password: <password>
```

This replaces the `--ask-become-pass` option.

---

# 3️⃣ Build the Execution Environment

## Build the Image

```bash
ansible-builder build -t kvm-libvirt-ee:1.0 -f execution-environment.yml
```

## Tag the Image

```bash
podman tag kvm-libvirt-ee:1.0 docker.io/<dockerhub username>/kvm-libvirt-ee:1.0
```

Push it to your container registry if required.

---

# 4️⃣ Run in Ansible Automation Platform (AAP)

##  Add the Execution Environment

1. Go to **Administration → Execution Environments**
2. Click **Create**
3. Name: `kvm-libvirt-ee`
4. Image:  
   ```
   docker.io/<dockerhub username>/kvm-libvirt-ee:1.0
   ```
5. Save

---

##  Create Credentials

### Machine Credential
1. Go to **Resources → Credentials**
2. Click **Create**
3. Credential Type: **Machine**
4. Provide:
   - Username (e.g., root or admin)
   - Password
   - Privilege Escalation Password 

Save.

---

##  Create Inventory (include hosts)

1. Go to **Resources → Inventories**
2. Click **Create**
3. Name your inventory (e.g., `kvm-hosts`)
4. Save


Supports:
- Classic `ansible-playbook`
- `ansible-navigator` with containerized EE
- Full deployment via Ansible Automation Platform (AAP)

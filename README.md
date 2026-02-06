run :
ansible-playbook playbooks/main.yml --ask-become-pass
admin password in the kvm host 


with special execution env :
ansible-navigator run main.yml   --eei docker.io/mejbria9/kvm-libvirt-ee:2.0   --execution-environment true   --container-engine podman   -i inventory/hosts.ini   -e @pass.yml

and add pass.yml which is a yml file with the admin password for --ask-become-pass => ansible_become_password: redhat


execution env : run => ansible-builder build -t kvm-libvirt-ee:2.0 -f execution-environment.yml
                        podman tag kvm-libvirt-ee:2.0 docker.io/mejbria9/kvm-libvirt-ee:2.0
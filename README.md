## Requirements

First, you have to copy your SSH keys to the VMs:

```bash
ssh-copy-id root@<ip-addres>
```

Then, to test that everything works correctly, you need to run:

```bash
ansible-playbook kubeplay.yml -i kubeinv.yml -u root --check
```

After it seems everything works, you can omit the `--check`.

---

## Considerations

For the playbook to work correctly, you need to have an unrestricted connection.

Also, I used domain names that you must set in your `/etc/hosts` file in order to access them.
For monitoring (KSM), I did this automatically, but if you want to deploy my app (IP Locator project), you must set it manually on your host.

You can change the IP addresses of your VMs in `kubeinv.yml`, and you can also set your preferred hostnames, cluster name, etc.

You can change the role and state as you prefer.
For example, in my setup, I have one master in init mode (it uses `init`, not `join`, and its role is `master`), and two workers (which have the `join` command; you can create a worker but choose not to join it yet).

---

## What does it do?

With this project, you can provision your homelab Kubernetes cluster and apply the Calico CNI, so you have a ready-to-use cluster. It also installs Ingress NGINX for you and deploys kube-state-metrics so you can monitor your cluster.

You can also use the monitoring task, which will run a Prometheus/Grafana/Alertmanager monitoring stack with Podman so you can monitor your cluster.
(Find the Grafana password in the `.env` file inside `/files`.)
I also added my Slack integration for alerting.

‼️ Don't mind the Slack webhook address — it is not usable anymore. 🙂

There are also three default dashboards:

1. One for Prometheus itself
2. One for kube-state-metrics
3. One for my IP Locator (Flask metrics) project (just for testing)

I also installed a reverse proxy on the master node to redirect every request with certain domain names to my cluster.

‼️ Yeah I didn't use MetalLB — **IT'S JUST A LAB!!!**

---

## Where to start?

You can run the playbook easily, and you can also deploy my IP Locator project on it just for testing.

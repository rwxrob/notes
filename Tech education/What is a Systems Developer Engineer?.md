**SysDE** stands for **Systems Development Engineer** — a role that combines the responsibilities of a **Software Engineer (SWE)** and a **Systems Administrator / DevOps / SRE**.
## **What a SysDE does**

A Systems Development Engineer builds **automated, scalable systems infrastructure** using **code**. This includes:

- Writing tools in Go, Python, Bash, etc.
- Automating infrastructure with Terraform, Ansible, Helm, and similar tools
- Managing and scaling Kubernetes clusters, CI/CD pipelines, and HPC systems
- Working across bare metal, containers, and cloud platforms (AWS, GCP, Azure)
- Ensuring reliability and observability while building the systems they support
## **Why not just call it DevOps or SRE?**

While there’s overlap, a **SysDE** emphasizes _engineering systems from scratch_, not just operating or maintaining them.

A typical SRE might focus more on:

- Incident response
- Uptime and alerting
- Runbooks and toil reduction

Whereas a **SysDE** often:

- Designs new systems and architecture
- Builds internal tools and platforms
- Creates clean, testable infrastructure code
- Writes libraries or CLIs for developer productivity
## **Real-world example**

> A company runs thousands of HPC workloads in Kubernetes.

> A SysDE writes a Go tool to auto-scale GPU nodes based on custom metrics, deploys it via Helm, monitors it with Prometheus, and makes it seamless for the data science team to consume.
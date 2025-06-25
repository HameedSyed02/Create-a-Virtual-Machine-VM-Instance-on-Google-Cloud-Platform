# Create-a-Virtual-Machine-VM-Instance-on-Google-Cloud-Platform
Create a Compute Engine VM instance in GCP using the Google Cloud Console and `gcloud` CLI.

---

## ✅ Prerequisites

Before you begin:

- A [Google Cloud account](https://cloud.google.com/)
- Billing enabled on your GCP project
- `gcloud` CLI installed (optional, for CLI users) → [Install guide](https://cloud.google.com/sdk/docs/install)

---

## 🖥️ Method 1: Create VM via Google Cloud Console

1. Go to the [VM Instances page](https://console.cloud.google.com/compute/instances).
2. Click **“Create Instance”**.
3. Configure the instance:
   - **Name**: `my-vm-instance`
   - **Region/Zone**: e.g., `us-central1-a`
   - **Machine Type**: `e2-medium` (2 vCPU, 4 GB RAM)
   - **Boot Disk**:
     - Image: `Debian`, `Ubuntu`, etc.
     - Type: `Balanced persistent disk (pd-balanced)`
     - Size: 10 GB (or more)
   - **Firewall**: Check both **Allow HTTP** and **Allow HTTPS**
4. Click **Create**.

⏳ Wait a few seconds for the VM to be provisioned.

---

## 🔧 Method 2: Create VM Using `gcloud` CLI

Make sure you're authenticated:

```bash
gcloud auth login
```
Set your project:
```bash
gcloud config set project YOUR_PROJECT_ID
```

Create the instance:
```bash
gcloud compute instances create my-vm-instance \
  --zone=us-central1-a \
  --machine-type=e2-medium \
  --boot-disk-type=pd-balanced \
  --boot-disk-size=10GB \
  --image-family=debian-11 \
  --image-project=debian-cloud \
  --tags=http-server,https-server
```
🔌 Connect to Your VM
Via Console:

Click SSH button next to your VM.

Via CLI:
```bash
gcloud compute ssh my-vm-instance --zone=us-central1-a
```
 Install a Web Server
Once connected:
```bash
sudo apt update
sudo apt install apache2 -y
```

Cleanup
To delete the VM when you're done:
```bash
gcloud compute instances delete my-vm-instance --zone=us-central1-a
```





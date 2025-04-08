# Configuring-Active-Directory-within-Azure-VMs

# Lab: Setup Domain Controller in Azure

## Objective:
In this lab, you will set up a Windows Server 2022 Domain Controller and a Windows 10 client machine (Client-1) in Azure. This will simulate a small Active Directory network.

---

## Step 1: Create a Resource Group

1. In the Azure portal, click on **"Resource groups"** in the left-hand menu.
2. Click **"Add"** to create a new resource group.
3. Name the resource group: `AD-Lab-ResourceGroup`
4. Select your region and click **"Review + Create"** to create the resource group.

---

## Step 2: Create a Virtual Network and Subnet

1. Go to the **"Virtual Networks"** section in Azure and click **"Add"**.
2. Name your Virtual Network: `AD-Lab-VNet`
3. Set the region to the same as your resource group.
4. Create a new subnet with the name: `Subnet-1`, and use the address range: `10.0.0.0/24`.
5. Click **"Review + Create"** to create the virtual network.

---

## Step 3: Create the Domain Controller VM (Windows Server 2022)

1. Go to **"Virtual Machines"** in the Azure portal and click **"Add"**.
2. Select the following options:
   - **VM Name:** `DC-1`
   - **Region:** Select the same region as your Resource Group.
   - **Image:** Windows Server 2022 Datacenter
   - **Size:** Select an appropriate size for your VM, e.g., **Standard DS2 v2**.
   - **Username:** `labuser`
   - **Password:** `Cyberlab123!`
3. Under **Networking**, select the virtual network you created earlier (`AD-Lab-VNet`) and subnet (`Subnet-1`).
4. After the VM is created, go to the **"Networking"** tab of `DC-1` and set the **NIC Private IP** to be **static**.
5. Go to the **"Networking"** tab and disable the **Windows Firewall** (for testing connectivity).
6. Click **"Review + Create"** to create the VM.

---

## Step 4: Create the Client-1 VM (Windows 10)

1. Go to **"Virtual Machines"** in the Azure portal and click **"Add"**.
2. Select the following options:
   - **VM Name:** `Client-1`
   - **Region:** The same as your domain controller VM.
   - **Image:** Windows 10
   - **Size:** Choose an appropriate size, e.g., **Standard B1s**.
   - **Username:** `labuser`
   - **Password:** `Cyberlab123!`
3. Under **Networking**, select the virtual network `AD-Lab-VNet` and subnet `Subnet-1` (the same as `DC-1`).
4. Click **"Review + Create"** to create the Client VM.

---

## Step 5: Set DNS for Client-1

1. After the Client-1 VM is created, navigate to the **Networking** tab in the Azure portal.
2. Set the **DNS servers** for Client-1 to use the **Private IP address of DC-1** (for example, `10.0.0.4`).
3. Click **"Save"** to apply the settings.

---

## Step 6: Restart Client-1 VM

1. From the Azure portal, go to **"Virtual Machines"**.
2. Select **Client-1** and click **"Restart"** to restart the VM and apply the DNS settings.

---

## Step 7: Test Connectivity from Client-1

1. Log into **Client-1** via Remote Desktop.
2. Open **Command Prompt** or **PowerShell** on Client-1 and attempt to ping `DC-1`'s private IP address (e.g., `ping 10.0.0.4`).
   - The ping should succeed if the connectivity is correct.
3. To verify the DNS settings, run the following command in **PowerShell**: 
   ```bash
   ipconfig /all

   
This guide provides clear, step-by-step instructions for setting up both the Domain Controller and Client VM in Azure, with all the relevant details included.


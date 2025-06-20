#!/bin/bash

# --------- Variables ----------
RESOURCE_GROUP="MyResourceGroup"
LOCATION="centralindia"
VNET_NAME="MyVnet"
SUBNET_NAME="MySubnet"
VM_NAME="MyVM"
USERNAME="azureuser"
PASSWORD="MySecurePass123!"

# --------- Create Resource Group ----------
az group create --name $RESOURCE_GROUP --location $LOCATION

# --------- Create VNet & Subnet ----------
az network vnet create \
  --resource-group $RESOURCE_GROUP \
  --name $VNET_NAME \
  --address-prefix 10.0.0.0/16 \
  --subnet-name $SUBNET_NAME \
  --subnet-prefix 10.0.0.0/24

# --------- Create Public IP ----------
az network public-ip create \
  --resource-group $RESOURCE_GROUP \
  --name "${VM_NAME}PublicIP"

# --------- Create NSG & RDP Rule ----------
az network nsg create \
  --resource-group $RESOURCE_GROUP \
  --name "${VM_NAME}NSG"

az network nsg rule create \
  --resource-group $RESOURCE_GROUP \
  --nsg-name "${VM_NAME}NSG" \
  --name "Allow-RDP" \
  --protocol tcp \
  --priority 1000 \
  --destination-port-range 3389 \
  --access allow \
  --direction inbound

# --------- Create NIC ----------
az network nic create \
  --resource-group $RESOURCE_GROUP \
  --name "${VM_NAME}NIC" \
  --vnet-name $VNET_NAME \
  --subnet $SUBNET_NAME \
  --network-security-group "${VM_NAME}NSG" \
  --public-ip-address "${VM_NAME}PublicIP"

# --------- Create VM ----------
az vm create \
  --resource-group $RESOURCE_GROUP \
  --name $VM_NAME \
  --nics "${VM_NAME}NIC" \
  --image Win2019Datacenter \
  --admin-username $USERNAME \
  --admin-password $PASSWORD \
  --location $LOCATION \
  --size Standard_B1s \
  --output json

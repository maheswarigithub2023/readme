# Resource group for acr
resource "azurerm_resource_group" "rg_acr" {
  name     = "rg-acr-${var.global_settings.resourcetype}-${var.global_settings.environment}-${var.global_settings.location}-${var.global_settings.environment_instance}"
  location = var.global_settings.location
  tags     = var.global_settings.tags
}

resource "azurerm_container_registry" "acr" {
  name                          = "acr${var.global_settings.environment}${var.global_settings.location}${var.global_settings.environment_instance}"
  resource_group_name           = azurerm_resource_group.rg_acr.name
  location                      = azurerm_resource_group.rg_acr.location
  sku                           = var.acr_settings.sku
  admin_enabled                 = var.acr_settings.admin_enabled
  public_network_access_enabled = var.acr_settings.public_network_access_enabled
}

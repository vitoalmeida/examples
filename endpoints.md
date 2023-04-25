# Endpoints
<!-- /api/vaultData -->
## GET /vault/${vaultId} ✔
 - returns_a_404_when_non_existing_vault_id_provided
 - tested 200 at check_initial_data
	
<!-- /api/createVault -->
## POST /vault ✔
 - returns_a_400_when_data_is_missing
 - returns_a_404_when_user_id_not_exists
 - returns_a_400_when_fields_are_present_but_invalid
 - returns_a_201_when_persists_the_new_vault
 *Criar teste para verificar se foi criado uma role*

<!-- /api/userVaults -->
## GET user/${userId}/vaults ✔
- rever todos os testes

<!-- /api/userWallets -->
## GET /vault/${vaultId}/wallets ✔
- rever todos os testes

<!-- /api/userExchanges -->
## GET /vault/${vaultId}/exchanges ✔
- rever todos os testes
 
<!-- /api/vault/settings -->
## GET /vault/${vaultId}/contacts ✔
- rever todos os testes

## GET /vault/{vault_id}/role-with-permissions ✔
- returns_404_when_non_existing_vault_id_provided_to_roles 
- returns_200_when_data_is_successfully_returned_from_roles 

## POST /vault/role-with-permissions ✔
- returns_201_when_role_created_with_empty_permissions_array
- returns_201_when_role_created_with_permissions
- returns_400_when_role_created_with_duplicate_permissions
- returns_404_when_role_created_with_mix_of_valid_and_invalid_permission_ids
- returns_400_when_fields_are_present_but_invalid
- returns_400_when_fields_are_missing

## PUT /vault/role-with-permissions/${roleId} ✔
- returns_200_when_role_updated_with_empty_permissions_array
- returns_200_when_role_updated_with_permissions
- returns_400_when_role_updated_with_duplicate_permissions
- returns_404_when_role_updated_with_mix_of_valid_and_invalid_permission_ids
- returns_400_when_fields_are_present_but_invalid_on_role_update
- returns_400_when_fields_are_missing_on_role_update
	
## DELETE /vault/role-with-permissions/${roleId}?newRoleId="" ✔
- returns_400_when_providing_invalid_new_role_id
- returns_404_when_non_existing_role_id
- returns_404_when_providing_invalid_role_id
- returns_204_when_deleting_existing_role_without_new_role_id
- returns_204_when_deleting_existing_role_and_update_access_with_new_role_id

## PUT /access/${accessId}
- returns_400_when_fields_are_present_but_invalid_on_role_update
- returns_400_when_fields_are_missing_on_role_update
- returns_400_when_access_updated_with_missing_data
- returns_404_when_access_updated_with_invalid_foreign_key
- returns_204_when_access_updated_successfully
- returns_204_and_updates_data_when_access_updated_successfully

## GET /vault/${vaultId}/admin-log 
*!!! need to verify with designers*

# HTTP verbs test pattern:
### POST 
- 400 if data is missing or invalid
- 404 if it has one or more fk's in payload or id in query parameter but not found in database
- 201 if uptade a record

### PUT 
- 400 if data is missing or invalid
- 404 if it has one or more fk's in payload or id in query parameter but not found in database
- 200 if created a record

### GET
- 404 if not found query parameters on database
- 200 if return data even if empty

### DELETE
- 404 if not found any of query parameters on database
- 204 if return data is sucessfuly deleted

*Obs.:*
*- If the endpoint returns data with table joins, it's nice to test the returned data with a mock*

| Service | Endpoint Path                            | HTTP Method |
|---------|------------------------------------------|-------------|
| access  | /access/{accessId}                       | PUT         |
| vault   | /vault                                   | POST        |
| vault   | /vault/{vaultId}                         | GET         |
| vault   | /vault/{vaultId}/wallets                 | GET         |
| vault   | /vault/{vaultId}/exchanges               | GET         |
| vault   | /vault/role-with-permissions             | POST        |
| vault   | /vault/role-with-permissions/{vaultId}   | GET         |
| vault   | /vault/role-with-permissions/{roleId}    | DELETE      |
| vault   | /vault/role-with-permissions/{roleId}    | PUT         |
| vault   | /vault/{vaultId}/contacts                | GET         |
| user    | /user/{userId}/vaults                    | GET         |

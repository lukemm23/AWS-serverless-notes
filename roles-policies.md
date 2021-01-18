# Roles and Policies:

- all end points needs role and policies attached to perform purposed functions / lambda functions with access to database (DynamoDB).

1. go to IAM
2. select policies > create policy > select technology(DynamoDB) > select action type > copy and paste ARN (can be found inside database table overview). > name policy and create.
3. select roles > choose role wanting to edit or create new role choose lambda if using lambda function. > select created policy > name new role if needed.

- to change role from lambda:

1. choose function > go to permissions > click edit > swap from available role.

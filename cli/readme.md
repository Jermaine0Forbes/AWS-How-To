# CLI How To

-[how to setup a cli on your computer][setup-cli]
-[how to check the version of your cli][ver-cli]

## Dynamo DB
- [how to list out tables][dyn-list]
- [how to create dynamo table][dyn-create]
- [how to insert item in dynamodb][dyn-ins]
- [how to list items in a dynamodb table][dyn-list-items]
- [how to delete a dynamodb table][dyn-delete]

[dyn-delete]:#how-to-delete-a-dynamodb-table
[dyn-list-items]:#how-to-list-items-in-a-dynamodb-table
[dyn-ins]:#how-to-insert-item-in-dynamodb
[dyn-create]:#how-to-create-dynamo-table
[dyn-list]:#how-to-list-out-tables
[ver-cli]:#how-to-check-the-version-of-your-cli
[setup-cli]:#how-to-setup-a-cli-on-your-computer
[home]:#cli-how-to


### how to delete a dynamodb table

<details>
<summary>
View Content
</summary>

:link: **Reference**

- [Deleting the Amazon DynamoDB tables](https://docs.aws.amazon.com/solutions/latest/research-service-workbench-on-aws/deleting-the-amazon-dynamodb-tables.html)

```
aws dynamodb delete-table -–table-name <tablename>
```

</details>
[go back :house:][home]


### how to list items in a dynamodb table

<details>
<summary>
View Content
</summary>


:link: **Reference**

- [aws cli](https://docs.aws.amazon.com/cli/latest/reference/dynamodb/scan.html#examples)

In windows
```
aws dynamodb scan ^
    --table-name Users
```

</details>
[go back :house:][home]

### how to insert item in dynamo db

<details>
<summary>
View Content
</summary>

:link: **Reference**

- [aws cli](https://docs.aws.amazon.com/cli/latest/reference/dynamodb/put-item.html#examples)

Creating anything in aws cli sucks so it's much better to just do it through the command console,
sdk, or cdk

In windows
```
aws dynamodb put-item ^
    --table-name Users  ^
    --item ^
        "{\"Name\": {\"S\": \"John Doe\"}, \"Id\": {\"N\": \"1\"}}"
    --return-consumed-capacity TOTAL ^
    --return-item-collection-metrics SIZE
```

</details>
[go back :house:][home]


### how to create dynamo table

<details>
<summary>
View Content
</summary>

:link: **Reference**

- [Create a table in DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/getting-started-step-1.html)

In windows
```
aws dynamodb create-table ^
    --table-name Users ^
    --attribute-definitions ^
        AttributeName=Id,AttributeType=N ^
        AttributeName=Name,AttributeType=S ^
    --key-schema ^
        AttributeName=Id,KeyType=HASH ^
        AttributeName=Name,KeyType=RANGE ^
    --provisioned-throughput ^
        ReadCapacityUnits=5,WriteCapacityUnits=5 ^
    --table-class STANDARD
```

In linux
```
aws dynamodb create-table \
    --table-name Music \
    --attribute-definitions \
        AttributeName=Artist,AttributeType=S \
        AttributeName=SongTitle,AttributeType=S \
    --key-schema \
        AttributeName=Artist,KeyType=HASH \
        AttributeName=SongTitle,KeyType=RANGE \
    --provisioned-throughput \
        ReadCapacityUnits=5,WriteCapacityUnits=5 \
    --table-class STANDARD
```

</details>
[go back :house:][home]

### how to list out tables

<details>
<summary>
View Content
</summary>
:link: **Reference**

- [aws cli examples](https://docs.aws.amazon.com/cli/latest/reference/dynamodb/list-tables.html#examples)

```
aws dynamodb list-tables
```

</details>
[go back :house:][home]

### how to check the version of your cli

<details>
<summary>
View Content
</summary>

:link: **Reference**

- [Installing, Updating, and Uninstalling the AWS CLI version 1 on Windows](https://docs.aws.amazon.com/cli/v1/userguide/install-windows.html#msi-on-windows)

Type in command prompt

```
aws --version
```

</details>
[go back :house:][home]

### how to setup a cli on your computer

<details>
<summary>
View Content
</summary>

:link: **Reference**

- [Download and run the AWS CLI MSI installer for Windows (64-bit)](https://awscli.amazonaws.com/AWSCLIV2.msi)
- []()

1. If on windows, [download and install](https://awscli.amazonaws.com/AWSCLIV2.msi) the aws cli msi installer
    - If you have another OS, go to [this page](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) in order to install the appropriate software

</details>
[go back :house:][home]




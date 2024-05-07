# terraform-basics

# Commands
1. terraform init
2. terraform plan
3. terraform apply
4. terraform show
5. terraform destroy
6. terraform validate
7. terraform fmt
8. terraform show -json
9. terraform providers
10. terraform output
11. terraform refresh

## HCL(Hashicorp configuration language)

### Sample hcl syntex
```ruby
<block> <parameters> {
  key1 = value1,
  key2 = value2
}
```

HCL file consists of blockes and arguments

**Note** : An block is defined in bracket, and it contains set of arguments in key and value formate. which represents the configuration data.

![image](https://github.com/rajesh2475/terraform-basics/assets/24488810/5c9420d5-f39e-405d-aa72-5f7662b9b084)


Providers
- providers are available at https://registry.terraform.io/
- all the providers used in the terraform files will be downloaded when you execute terraform init
- by default terraform will install latest version

Types of files which can be created
| File Name  | Purpose |
| ------------- | ------------- |
| main.tf  | The main configuration file that contains some source definitions  |
| variables.tf  | Contains variable declarations   |
| output.tf  | Contains outputs from resources  |
| provider.tf  | Contains provider definitions  |


# Input variables (variables.tf):
### Sample variable declaration 
```ruby
variable <variable_name> {
  default = "variable_value",
}
```
We can also define type and description in variable declaration 

### To use the variable in resource file
  ```
    var.variable_name
  ```

## Types of variables 
| type  | example |
| ------------- | ------------- |
| string  | "<string value>"  |
| numberr  |1  |
| bool  | true/false  |
| any  | default value  |
| list  | ["1", "2"]  |
| map  | key1 = value1<br />key2 = value2  |
| object  | Complex data structure  |
| tuple  | Complex data structure  |


### Variable examples
#### List
```ruby
  variable "users" {
    default = ["user1", "user2", "user3"]
    type = list(string)
  }
```
#### map
```ruby
  variable "user" {
    default = {
      name = "user1"
    }
    type = map(string)
  }
```
#### Set (list without duplicates)
```ruby
  variable "users" {
    default = ["user1", "user2", "user3"]
    type = set(string)
  }
```
#### Object
```ruby
  variable "user" {
    default = {
      name = "user1"
      age = 30
      marks = [10,20,30]
      pass = false
    }
    type = object({
        name = string
        age = number
        marks = list(number)
        pass = bool
    })
  }
```
#### tuple (list with different item data types)
```ruby
  variable "users" {
    default = ["user1", 21, true]
    type = tuple[string, number, bool]
  }
```

## Different ways to define variables
### example create an variable called "userName"
1. create in variables.tf file
    ```
      variable "userName"{
        default = "user1"
      }
    ```
2. create an env variable as
    ```
      export TF_VAR_userName=user1
    ```
3. create variable in terraform.tfvars file
    ```
      userName = "user1"
    ```
4. pass variable while performing terraform apply
    ```
      terraform apply -var "userName="user1""
    ```
## Order of priority
1. loads the env variables
2. variables in terraform.tfvars file
3. command line flag (-var (while doing terraform apply))
**Note** - It will override the values down the order




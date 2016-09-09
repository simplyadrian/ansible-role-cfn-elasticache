# ansible-role-cfn-elasticache

## Playbook Parameters
| Parameter        | Required           | Default  | Description |
| ------------- |:---------:| -----------------:| -------------------------------------------------------------------------:|
| elasticache_stack_name | yes | none | Name for the ElastiCache CloudFormation stack |
| elasticache_stack_description | yes | none | Description of the CloudFormation stack |
| elasticache_tags | yes | none | Tags to apply to the CloudFormation stack |
| elasticache_cluster_name | yes | none | Name of the ElastiCache cluster |
| elasticache_vpc | yes | none | VPC in which the ElastiCache cluster will live |
| elasticache_subnet_group | no | none | Name of the Subnet Group to use with the cluster |
| elasticache_engine | yes | none | The engine to use with the cluster (redis/memcached) |
| elasticache_port | yes | 6379 | Port on which to run the cluster |
| elasticache_az_mode | yes (redis only) | cross-az | Whether to use cross-az or single-az for the cluster |
| elasticache_use_replicaton_group | no | none | Whether to use a replication group |
| elasticache_failover_enabled | conditional; if elasticache_use_replicaton_group is "true", then required | true | Whether to enable failover for the cluster |
| elasticache_preferred_zones | yes | us-west-2a, us-west-2b, us-west-2c | The preferred zones to use with the cluster |
| elasticache_node_type | yes | cache.m3.medium | The instance type to use with the cluster instances |
| elasticache_node_quantity | yes | 5 | The number of nodes to use in the cluster |
| elasticache_disable_rollback | yes | true | Whether to prevent rollback of cluster changes |
| elasticache_state | yes | present | Whether the CloudFormation stack should be <strong>present</strong> or <strong>absent</strong> | 
| elasticache_build_dir | yes | <strong>playbook_dir</strong>/build | Directory in which to deposit temporary build artifacts |
| elasticache_template_src | yes | <strong>playbook_dir</strong>/templates/elasticache.j2.json | Source template for CloudFormation stack |
| elasticache_template_dest_tmp | yes | <strong>elasticache_build_dir</strong>/elasticache.json-tmp | Name of the temporary destination template |
| elasticache_template_dest | yes | <strong>elasticache_build_dir</strong>/elasticache.json | Name of the final destination template |

## Example Playbook
```
- hosts: localhost
  vars:
    elasticache_cluster_name: test-cluster
    elasticache_vpc: vpc-1234567
    elasticache_subnet_group: "Test"
    elasticache_stack_description: "ElastiCache cluster test"
    elasticache_engine: redis
    elasticache_tags:
      "test" : "test"
    elasticache_stack_name: "test-elasticache-stack"
  roles:
    -  ansible-role-module-cfn-elasticache
```

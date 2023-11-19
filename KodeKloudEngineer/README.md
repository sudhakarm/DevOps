KodeKloud Engineering tasks

# SSH commands


| Service Name                    | Command               | Password    |
| ------------------------------- | --------------------- | ----------- |
| Nautilus App 1                  | `ssh tony@stapp01`    | Ir0nM@n     |
| Nautilus App 2                  | `ssh steve@stapp02`   | Am3ric@     |
| Nautilus App 3                  | `ssh banner@stapp03`  | BigGr33n    |
| Nautilus HTTP LBR               | `ssh loki@stlb01`     | Mischi3f    |
| Nautilus DB Server              | `ssh peter@stdb01`    | Sp!dy       |
| Nautilus Storage Server         | `ssh natasha@ststor01`| Bl@kW       |
| Nautilus Backup Server          | `ssh clint@stbkp01`   | H@wk3y3     |
| Nautilus Mail Server            | `ssh groot@stmail01`  | Gr00T123    |
| Jump Server to Access Stork DC  | `ssh thor@jump_host`  | mjolnir123  |
| Jenkins Server for CI/CD        | `ssh jenkins@jenkins` | j@rv!s      |


| Direct command                                                                 | Password    |
| ------------------------------------------------------------------------------ | ----------- |
| `sshpass -p "Ir0nM@n"  ssh -tt -o StrictHostKeyChecking=no  tony@stapp01`      | Ir0nM@n     |
| `sshpass -p "Am3ric@"  ssh -tt -o StrictHostKeyChecking=no  steve@stapp02`     | Am3ric@     |
| `sshpass -p "BigGr33n"  ssh -tt -o StrictHostKeyChecking=no  banner@stapp03`   | BigGr33n    |
| `sshpass -p "Mischi3f"  ssh -tt -o StrictHostKeyChecking=no  loki@stlb01`      | Mischi3f    |
| `sshpass -p "Sp!dy"  ssh -tt -o StrictHostKeyChecking=no  peter@stdb01`        | Sp!dy       |
| `sshpass -p "Bl@kW"  ssh -tt -o StrictHostKeyChecking=no  natasha@ststor01`    | Bl@kW       |
| `sshpass -p "H@wk3y3"  ssh -tt -o StrictHostKeyChecking=no  clint@stbkp01`     | H@wk3y3     |
| `sshpass -p "Gr00T123"  ssh -tt -o StrictHostKeyChecking=no  groot@stmail01`   | Gr00T123    |
| `sshpass -p "mjolnir123"  ssh -tt -o StrictHostKeyChecking=no  thor@jump_host` | mjolnir123  |
| `sshpass -p "j@rv!s"  ssh -tt -o StrictHostKeyChecking=no  jenkins@jenkins`    | j@rv!s      |

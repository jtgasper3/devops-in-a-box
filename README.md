
```
docker run -it --rm -v ~/.vagrant.d/insecure_private_key:/private_key -v $(pwd):/ansible -w /ansible ansible/ansible-runner ansible-playbook project/test.yml -i inventory/hosts
```

```
ssh -i ~/.vagrant.d/insecure_private_key vagrant@10.
```



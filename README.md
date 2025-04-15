
# amazon-vpc-cni-k8s

This repository is a forked version of [amazon-vpc-cni-k8s](https://github.com/aws/amazon-vpc-cni-k8s) that can be run on self-hosted EC2.

The maintenance of this repository is carried out as needed, so it may not always be the latest version. If the versions are different, we recommend that you check the changed files and apply them yourself.

## Setup

Download the latest version of the [yaml](./config/master/aws-k8s-cni-self-hosted.yaml) and apply it to the cluster.

Generate ecr secret, iam needs ecr registry permission.

```bash
kubectl create secret docker-registry aws-registry-secret \
  --docker-server=602401143452.dkr.ecr.us-west-2.amazonaws.com \
  --docker-username=AWS \
  --docker-password=$(aws ecr get-login-password --region us-west-2) \
  --namespace=kube-system
```

Now, apply yaml.

```bash
kubectl apply -f aws-k8s-cni-self-hosted.yaml
```

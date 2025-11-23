# ML102 k8s example

## Running it

The pod will de deployed to the `kai-test` namespace and will be named `ml102-test`.
You may need to change the name of the pod if there is already one with the same name running (`kubectl -n kai-test get pods`).

1. Make sure `kubectl` is configured
2. Edit *ml102-example-pod.yaml* if required
3. Launch the pod with:
   ```
   kubectl apply -f ml102-example-pod.yaml
   ```
4. Check status of the pod (changing the name of the pod if required):
   ```
   kubectl -n kai-test describe pod ml102-test
   ```
5. Once the pod is running, setup port forwarding (changing name of the pod if required)
   ```
   kubectl -n kai-test port-forward pod/ml102-test 8888:8888
   ```
6. Connect to http://localhost:8888
   - notebooks should be available in the *notebooks* directory
   - open a Jupyter terminal and run `nvidia-smi` to check the GPU state

## Building the docker image

- The docker image should build automatically when you push changes
- Based on an older GPU enabled tensorflow image (the notebooks haven't been updated in a while and throw lots of warnings with newer tensorflow)


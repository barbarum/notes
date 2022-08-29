# Python Development

## pip 
```bash
pip freeze > requirements.txt # export pip installed package into requirements.txt
```

## FAQ 

1. `HTTPSConnectionPool(host='files.pythonhosted.org', port=443): Read timed out`
  
    It's due to slow connectivity to pypi official site in China. two solutions as follow: 
    ```bash
    pip install metricflow -i https://pypi.tuna.tsinghua.edu.cn/simple # reindex from tsinghua mirror pypi source
    pip install --default-timeout=1000 metricflow # enlarge default-timeout, the default value is 100
    ```

# & and wait

`&`를 사용하면 background로 실행 (서브프로세스)

```bash
sleep 5
```

`wait` 명령어를 통해 모든 서브프로세스가 다 끝날 떄 까지 기다릴 수 있음

```bash
sleep 7 &
sleep 3 &
wait
```

[Refer](https://twpower.github.io/189-run-multi-processes-in-shell-script-using-ampersand)

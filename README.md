# Scheduling Policy to the Linux Kernel

# O que é o Escalonador do Linux?
Antes de explicar o funcionamento do escalonador, é necessário conhecer sua definição. Em sistemas computacionais atuais, vários threads aguardam execução. Assim, o escalonador é um componente que ajuda a decidir qual processo será executado pela CPU em um determinado tempo. A maioria dos algoritmos de escalonamento é baseada em prioridades, sendo assim o escalonador do Linux desempenha um papel crucial na distribuição de recursos de CPU e E/S entre os processos em execução, visando oferecer um ambiente de execução equitativo e eficiente.



# Tutorial
1. Para começar, precisamos descobrir qual versão do kernel estamos executando no momento: 


```$ uname -r```


2. Obtenha o código do kernel Linux no site Kernel.org e usando o comando wget:

```$ cd /tmp```

```$ wget https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/snapshot/linux-2.6.24.y.tar.gz```


3. Extraia o arquivo .tar:

```$ tar -xzvf 2.6.24.y.tar.gz -C /usr/src```

```$ cd /usr/src/2.6.24.y```


4.  instalar a biblioteca curses e algumas outras ferramentas para nos ajudar a compilar :

```$ sudo apt-get install kernel-package libncurses5-dev fakeroot```


5. Aplicar as mudanças de implementação nas pastas sched.c,sched.h e chrtB.c:

/include/linux/sched.h  

/kernel/sched.c 

/usr/bin/chrt


6. Fazemos uma cópia da configuração do kernel para usar durante a compilação:

```$ cp boot/config-2.6.24-generic /usr/src/linux/.config```


7. Primeiro vamos fazer um make clean, só para ter certeza que está tudo pronto para a compilação:

```$ make-kpkg clean```


8. Em seguida, vamos realmente compilar o kernel. Isso levará um “TEMPO LONGO” talvez 40-50 minutos.

```$ fakeroot make-kpkg --initrd --append-to-version=-custom kernel_image kernel_headers```

Este processo criará dois arquivos .deb em /usr/src que contém o kernel


9. Observe que, ao executar os próximos comandos, isso definirá o novo kernel como o novo kernel padrão. Isso pode dar problema! Se sua máquina não inicializar, você pode pressionar Esc no menu de carregamento do GRUB e selecionar seu kernel antigo. Você pode então desabilitar o kernel em /boot/grub/menu.lst ou tentar compilar novamente. 

```$ dpkg -i linux-image-2.6.24-custom_2.6.24-custom-10.00.Custom_i386.deb```

```$ dpkg -i linux-headers-2.6.24-custom_2.6.24-custom-10.00.Custom_i386.deb```


10. Agora reinicie sua máquina. Se tudo funcionar, você deve estar executando seu novo kernel personalizado. Você pode verificar isso usando uname. Observe que o número exato será diferente em sua máquina.:

```$ uname -r```

2.6.24-custom


11. Para alterar a política de um processo para SCHED_BACKGROUND política em seu tempo de execução, comando usado: :

```$ chrt -g -p 0 < pid>```

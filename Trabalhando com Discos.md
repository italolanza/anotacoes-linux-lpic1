## Nomenclatura dos Discos
**sd**_x_*y* - SCSI (**S**mall **C**omputer **S**ystem **I**nterface) Disk. Onde *x* e a ordem que o disco foi reconhecido pelo Kernel e *y* representa a partiçao do disco.

**Exemplo: **
> sda
├─sda1
└─sda2

<br>

## Sistemas de Arquivos
Para poder trabalhar com uma partiçao de disco, ela precisa ser formatada utilizando algum file system. Exemplo de FS's: ext, FAT, ZFS XFS.


Mount point: diretorio que e associado a um dispositivo de bloco.

<br>

## Particionamento de Discos

### MBR
**M**aster **B**oot **R**ecord ou `MBR`  um tipo de setor de inicialização armazenado em uma unidade de disco rígido ou outro dispositivo de armazenamento que contém informaçoes das partiçoes do disco, *file systems*, e tambem o código de computador necessário para iniciar o processo de inicialização. O MBR é criado quando um disco rígido é particionado, mas não está localizado _dentro de_ uma partição.

Limitaçoes:
+ 4 **Partiçoes Primarias**
ou
+ 3 **Partiçoes Primarias** + 1 **Particiçao Extendida**
	+ Uma **partiçao extendida** pode conter um **numro infinito** de **partiçoes logicas**.
		+ Partiçoes logicas sempre começam utilizando o numero 5


### GPT
**G**UID **P**artition **T**able é um tipo padrão de _layout_ de tabela de partição usado em um dispositivo de armazenamento físico, como uma unidade de disco rígido ou uma unidade de estado sólido, usando um _identificador único global_ chamado de [GUID](https://pt.wikipedia.org/wiki/GUID "GUID").

Limitaçoes:
+ 128 **Partiçoes Primarias**


### Swap
Tipo de partiçao no disco utilizada para funcionar como extençao da memoria RAM para que a mesma nao alcance o 100% de utilizaçao (causa reboot do sistema).


### LVM
**L**ogical **V**olume **M**anager é um método de alocar espaço do disco rígido em volumes lógicos que podem ser facilmente redimensionados, ao contrário das partições. Com o LVM, o disco rígido ou conjunto de discos rígidos é alocado em um ou mais _volumes físicos_. Um volume físico não pode ultrapassar mais de um disco.

Os volumes físicos são combinados em _grupos de volume lógico_ e sao divididos em _volumes lógicos_, aos quais são atribuídos pontos de montagem, tais como /home e /, e tipos de sistemas de arquivo.

![[utilizando-lvm-no-linux-01.png]]


Alguns comandos:
`pvs` - Lista os PVS criados
`vvs` - Lista os vgs criados
`lvs` - Lista os logical volumes criados
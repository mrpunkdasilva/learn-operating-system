# Prática 1

Nesta prática, vamos criar e configurar máquinas virtuais.

## Conhecendo ferramentas

Para fazer a virtualização de sistemas operacionais, temos alguns programas disponíveis:

- **Windows**: 
  - VirtualBox
  - VMWare
  - Parallels Desktop
- **Linux**:
  - VirtualBox
  - GNOME Boxes 
  - Virtual Machine Manager

> Há casos em que o VirtualBox falha por razões desconhecidas, então é melhor ter mais de uma opção disponível.
> {style="note"}

## Vamos começar

### Requisitos dos sistemas

Confira os requisitos dos sistemas operacionais que serão usados:

- [Windows 10](https://support.microsoft.com/pt-br/windows/requisitos-do-sistema-do-windows-10-6d4e9a79-66bf-7950-467c-795cf0386715)
- [Ubuntu Desktop](https://ubuntu.com/server/docs/system-requirements)

### Instalando a ferramenta

Vamos usar o VirtualBox.

- Para [Windows](https://download.virtualbox.org/virtualbox/7.1.6/VirtualBox-7.1.6-167084-Win.exe)
- Para [Linux](https://www.virtualbox.org/wiki/Linux_Downloads)

### Instalar ISOs (Windows e Ubuntu)

- [Windows](https://www.microsoft.com/pt-br/software-download/windows10ISO)

> Na ISO oficial do Windows, o link acima, vêm todas as versões.
> {style="note"}

- [Ubuntu Desktop](https://ubuntu.com/download/desktop)

### Criando Máquinas Virtuais
#### Windows {id="windows_1"}

1. Com o VirtualBox aberto, pressione: <kbd>CTRL</kbd> + <kbd>N</kbd>
> Você pode acessar a opção também por: `Machine > Add`
> {style="note"}
2. Definir nome, sistema e versão:

![Tela de criação de máquina virtual no VirtualBox](Captura de tela de 2025-02-28 19-52-13.png)

3. Agora vamos definir a memória RAM. É bom deixarmos no mínimo 4GB 

> Atente-se que computadores não lidam bem com números ímpares.
> {style="note"}

![Configuração de memória RAM para a máquina virtual](Captura de tela de 2025-02-28 19-52-35.png)

4. Agora definimos o espaço de armazenamento, disco rígido:

![Configuração de disco rígido para a máquina virtual](Captura de tela de 2025-02-28 19-52-57.png)

5. Com tudo criado, basta ir em `Finish`:

6. Temos então nossa primeira máquina virtual criada:

![Máquina virtual Windows criada no VirtualBox](Captura de tela de 2025-02-28 19-53-04.png)

---

#### Ubuntu {id="ubuntu_1"}

1. Com o VirtualBox aberto, pressione: <kbd>CTRL</kbd> + <kbd>N</kbd>
> Você pode acessar a opção também por: `Machine > Add`
> {style="note"}
2. Definir nome, sistema e versão:

![Tela de criação de máquina virtual Ubuntu no VirtualBox](Captura de tela de 2025-02-28 19-54-21.png)

3. Agora vamos definir a memória RAM. É bom deixarmos no mínimo 4GB 

> Atente-se que computadores não lidam bem com números ímpares.
> {style="note"}

![Configuração de memória RAM para a máquina virtual Ubuntu](Captura de tela de 2025-02-28 19-54-54.png)

4. Agora definimos o espaço de armazenamento, disco rígido:

![Configuração de disco rígido para a máquina virtual Ubuntu](Captura de tela de 2025-02-28 19-55-44.png)

5. Com tudo criado, basta ir em `Finish`:

6. Temos então nossa primeira máquina virtual criada:

![Máquina virtual Ubuntu criada no VirtualBox](Captura de tela de 2025-02-28 21-41-38.png)

### Logar nas VMs recém-criadas {id="logar-nas-vms-rec-m-criadas_1"}

Ao executar as máquinas, nenhum sistema será inicializado, já que não foi definida nenhuma ISO (Imagem de um Sistema Operacional). Assim, as máquinas ficam em seu estado puro, sem nenhum sistema operacional, e são inutilizáveis.

#### Windows {id="windows_2"}

![Tela inicial da máquina virtual Windows sem sistema operacional](Captura de tela de 2025-02-28 19-57-31.png)

#### Ubuntu {id="ubuntu_2"}

![Tela inicial da máquina virtual Ubuntu sem sistema operacional](Captura de tela de 2025-02-28 19-57-15.png)

### Configurando VMs para os SOs

Para tornar as VMs utilizáveis, precisamos definir as ISOs que serão as imagens do sistema usadas para instalar o sistema operacional.

#### Windows {id="windows_3"}

Com a máquina em execução e este pop-up aparecendo, selecionamos onde está a ISO do Windows que foi baixada nos passos anteriores:

![Seleção da ISO do Windows para instalação](Captura de tela de 2025-02-28 20-40-42.png)

#### Ubuntu

Com a máquina em execução e este pop-up aparecendo, selecionamos onde está a ISO do Ubuntu que foi baixada nos passos anteriores:

![Seleção da ISO do Ubuntu para instalação](Captura de tela de 2025-02-28 19-58-19.png)
### Logar nas VMs {id="logar-nas-vms_1"}

Agora, com tudo o que vimos, podemos fazer a instalação do sistema. Para isso, devemos logar ou entrar nas máquinas que criamos e então fazer as etapas de instalação do Windows e Ubuntu.

#### Windows {id="windows_4"}

![Tela inicial de instalação do Windows](VirtualBox_punk_windows_28_02_2025_20_41_23.png)

![Seleção de idioma, formato de hora e moeda, e layout de teclado](VirtualBox_punk_windows_28_02_2025_20_41_46.png)

![Botão "Instalar agora" para iniciar a instalação do Windows](VirtualBox_punk_windows_28_02_2025_20_41_53.png)

![Inserção da chave do produto Windows](VirtualBox_punk_windows_28_02_2025_20_42_11.png)

![Seleção da versão do Windows a ser instalada](VirtualBox_punk_windows_28_02_2025_20_42_15.png)

![Aceitação dos termos de licença do Windows](VirtualBox_punk_windows_28_02_2025_20_43_36.png)

![Escolha do tipo de instalação: Atualização ou Personalizada](VirtualBox_punk_windows_28_02_2025_20_43_46.png)

![Seleção do disco onde o Windows será instalado](VirtualBox_punk_windows_28_02_2025_20_43_53.png)

![Progresso da instalação do Windows](VirtualBox_punk_windows_28_02_2025_20_43_59.png)

![Reinicialização do sistema após a instalação inicial](VirtualBox_punk_windows_28_02_2025_20_49_12.png)

![Configuração inicial: Seleção de região](VirtualBox_punk_windows_28_02_2025_20_54_51.png)

![Configuração inicial: Confirmação do layout de teclado](VirtualBox_punk_windows_28_02_2025_20_55_27.png)

![Configuração inicial: Opção de adicionar um segundo layout de teclado](VirtualBox_punk_windows_28_02_2025_20_56_13.png)

![Configuração de rede: Conexão à internet](VirtualBox_punk_windows_28_02_2025_21_00_27.png)

![Configuração de conta: Opções de login](VirtualBox_punk_windows_28_02_2025_21_00_55.png)


![Definição de senha para a conta local](VirtualBox_punk_windows_28_02_2025_21_01_42.png)

![Configuração de perguntas de segurança](VirtualBox_punk_windows_28_02_2025_21_02_20.png)

![Configurações de privacidade: Escolha de permissões](VirtualBox_punk_windows_28_02_2025_21_02_37.png)

![Configuração de experiência personalizada](VirtualBox_punk_windows_28_02_2025_21_03_02.png)

![Configuração do assistente digital Cortana](VirtualBox_punk_windows_28_02_2025_21_03_11.png)

![Finalização da configuração do Windows](VirtualBox_punk_windows_28_02_2025_21_03_19.png)

![Área de trabalho do Windows após a instalação completa](VirtualBox_punk_windows_28_02_2025_21_07_43.png)

![Menu Iniciar do Windows recém-instalado e digite "Configurações"](VirtualBox_punk_windows_28_02_2025_21_07_55.png)

![Vá em "Sistema"](VirtualBox_punk_windows_28_02_2025_21_08_24.png)

![Na seção "Sobre" do sistema podemos ver as configurações da maquina que foi instalada](VirtualBox_punk_windows_28_02_2025_21_08_36.png)


#### Ubuntu {id="ubuntu_3"}

- Configurações de instalação:

![Assim que rodarmos a máquina, vai aparecer a tela do GRUB e então selecionamos a primeira opção](VirtualBox_punk_ubuntu_28_02_2025_19_58_36.png)

<note>
O GRUB (Grand Unified Bootloader) é o menu de inicialização que aparece quando você inicia o sistema Ubuntu. Ele permite que você escolha entre diferentes opções de inicialização.

- A primeira opção geralmente é "Ubuntu", que inicia o sistema normalmente.
- Outras opções podem incluir modos de recuperação ou versões anteriores do kernel.

Para a instalação padrão, selecione a primeira opção "Ubuntu" e pressione Enter para continuar.
</note>

![Selecionamos o idioma](VirtualBox_punk_ubuntu_28_02_2025_20_00_21.png)

![Na parte de Acessibilidade, é só se for necessário](VirtualBox_punk_ubuntu_28_02_2025_20_00_29.png)

![Selecionaremos agora o layout do teclado](VirtualBox_punk_ubuntu_28_02_2025_20_00_46.png)

![Deixe na forma padrão de conexão](VirtualBox_punk_ubuntu_28_02_2025_20_00_50.png)

![Aperte em "Next" ou "Próximo", deixe selecionada a forma padrão de instalação](VirtualBox_punk_ubuntu_28_02_2025_20_00_57.png)

![Deixe na forma interativa de instalação, ou seja, primeira opção](VirtualBox_punk_ubuntu_28_02_2025_20_01_06.png)

![Para a próxima parte, é onde definimos se queremos que ao instalar o Ubuntu sejam instalados aplicativos adicionais, além dos básicos como navegador e outros utilitários. Neste caso, deixe na opção padrão](VirtualBox_punk_ubuntu_28_02_2025_20_01_12.png)

![Nesta etapa, selecione todas as opções, que são para instalar softwares de terceiros e download de formatos de mídia adicionais](VirtualBox_punk_ubuntu_28_02_2025_20_01_18.png)

![Nesta parte é a definição de se iremos instalar limpando o disco ou se faremos o particionamento do disco. Deixe a opção como padrão e aperte em next](VirtualBox_punk_ubuntu_28_02_2025_20_01_27.png)

![Agora na parte de criação de conta, defina suas credenciais](VirtualBox_punk_ubuntu_28_02_2025_20_03_04.png)

![Agora é só fazermos a configuração do fuso horário, ou seja, do tempo que o computador irá usar](VirtualBox_punk_ubuntu_28_02_2025_20_03_28.png)

![Nesta página será apenas para mostrar o resumo da instalação, uma visão geral das configurações para instalação](VirtualBox_punk_ubuntu_28_02_2025_20_03_34.png)

![Aqui é a etapa em que o sistema será instalado, pode demorar uns 30 minutos](VirtualBox_punk_ubuntu_28_02_2025_20_03_38.png)

![Com a etapa anterior concluída, o sistema já foi instalado e já podemos reiniciar a máquina](VirtualBox_punk_ubuntu_28_02_2025_20_29_53.png)

![Ao reiniciarmos a máquina, aparece então a tela de login do usuário que foi criado](VirtualBox_punk_ubuntu_28_02_2025_20_32_34.png)

![Ao logarmos, temos a visão desta tela](VirtualBox_punk_ubuntu_28_02_2025_20_34_46.png)

![Nessa parte, basta passarmos adiante - clique em Skip ou Prosseguir](VirtualBox_punk_ubuntu_28_02_2025_20_35_05.png)

![Aperte a tecla Super do seu teclado e digite "settings" ou "configurações" e aperte no primeiro item](VirtualBox_punk_ubuntu_28_02_2025_20_37_43.png)

![Vá na parte inferior do menu lateral esquerdo e aperte em "System" ou "Sistema" e em seguida aperte em "About" ou "Sobre"](VirtualBox_punk_ubuntu_28_02_2025_20_37_55.png)

![Assim podemos visualizar as informações do sistema que está instalado](VirtualBox_punk_ubuntu_28_02_2025_20_38_18.png)
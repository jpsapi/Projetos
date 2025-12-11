# Projetos

### 🌐 Automação de Rede: Gerenciamento de Switches com Ansible

Este projeto demonstra o uso do Ansible para alcançar **configuração de rede zero-touch** e garantir a conformidade dos dispositivos críticos da infraestrutura.

O foco aqui é na **gestão do estado** dos *switches*, não apenas na execução de comandos.

#### 🎯 Principais Objetivos da Automação

1.  **Padronização de Configuração:** Aplicação de templates Jinja2 para garantir que todos os *switches* mantenham uma configuração base consistente (VLANs, NPT, Logging).
2.  **Idempotência de Rede:** Utilização de módulos de rede específicos (ex: `cisco.ios.ios_config`, `community.network.cli_config`) que garantem que apenas mudanças necessárias sejam aplicadas, minimizando *outages*.
3.  **Gestão de Credenciais Segura:** Integração com **Ansible Vault** para gerenciar credenciais SSH/Telnet e garantir que as informações sensíveis dos dispositivos nunca sejam expostas em texto simples.

#### 🛠️ Tecnologias e Ferramentas Utilizadas

| Ferramenta | Uso |
| :--- | :--- |
| **Ansible** | Orquestração e execução de *playbooks*. |
| **Ansible Vault** | Criptografia de senhas e *secrets* de dispositivos. |
| **Módulos de Rede** | Cisco IOS, Arista EOS, Juniper Junos (Adapte conforme o seu fabricante). |

#### 🔑 Demonstrações Chave (Ver Playbooks)

* **`playbook_backup_config.yml`:** Automação de backup diário da configuração em execução (*running-config*) de todos os dispositivos.
* **`role_aplicar_vlan.yml`:** Role idempotente para adicionar, remover ou modificar VLANs, garantindo que o estado final seja o desejado.
* **`inventory_dynamic.ini`:** Exemplo de como segmentar *switches* por grupos (e.g., `core`, `access`) para aplicação de políticas específicas.

---

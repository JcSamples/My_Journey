
`Strategic Intelligence` is characterized by:

- Being consumed by C-suite executives, VPs, and other company leaders
- Aiming to align intelligence directly with company risks to inform decisions
- Providing an overview of the adversary's operations over time
- Mapping TTPs and Modus Operandi (MO) of the adversary
- Striving to answer the Who? and Why?
- `Example`: A report containing strategic intelligence might outline the threat posed by APT28 (also known as Fancy Bear), a nation-state actor linked to the Russian government. This report could cover the group's past campaigns, its motivations (such as political espionage), targets (like governments, military, and security organizations), and long-term strategies. The report might also explore how the group adapts its tactics and tools over time, based on historical data and the geopolitical context.

`Operational Intelligence` is characterized by:

- Also including TTPs of an adversary (similar to strategic intelligence)
- Providing information on adversary campaigns
- Offering more detail than what's found in strategic intelligence reports
- Being produced for mid-level management personnel
- Working towards answering the How? and Where?
- `Example`: A report containing operational intelligence can provide detailed analysis of a ransomware campaign conducted by the REvil group. It would include how the group gains initial access (like through phishing or exploiting vulnerabilities), its lateral movement tactics (such as credential dumping and exploiting Windows admin tools), and its methods of executing the ransomware payload (maybe after hours to maximize damage and encrypt as many systems as possible).

`Tactical Intelligence` is characterized by:

- Delivering immediate actionable information
- Being provided to network defenders for swift action
- Including technical details on attacks that have occurred or could occur in the near future
- `Example`: A report containing tactical intelligence could include specific IP addresses, URLs, or domains linked to the REvil command and control servers, hashes of known REvil ransomware samples, specific file paths, registry keys, or mutexes associated with REvil, or even distinctive strings within the ransomware code. This type of information can be directly used by security technologies and incident responders to detect, prevent, and respond to specific threats.



# RAT

RAT (Remote Access Trojan)

**`RAT Characteristics`**

The RAT deployed in these attacks is modular, implying that it can be augmented with an infinite range of capabilities. While only a few features are accessible once the RAT is staged, we have noted the use of tools that capture screen dumps, execute [Mimikatz](https://attack.mitre.org/software/S0002/), provide an interactive `CMD shell` on compromised machines, and so forth.

WINRM

1. **Segurança**: O WinRM utiliza autenticação baseada em Kerberos ou autenticação baseada em certificados para garantir a segurança da comunicação entre sistemas. Ele também oferece suporte a criptografia de dados usando SSL/TLS para proteger as informações transmitidas pela rede.
    
2. **Confiabilidade**: O WinRM é projetado para ser confiável e robusto, suportando a detecção de erros e a recuperação automática em caso de falhas de comunicação.
    
3. **Integração com Ferramentas de Gerenciamento**: O WinRM é integrado com várias ferramentas de gerenciamento e automação, como o Windows PowerShell, o System Center Configuration Manager (SCCM) e o Windows Remote Server Administration Tools (RSAT), facilitando a administração remota de sistemas Windows.
    
4. **Protocolo Baseado em Web**: O WinRM utiliza o protocolo HTTP ou HTTPS para comunicação, o que facilita a comunicação através de firewalls e proxies corporativos.
5. 
#SITE DPE



<!DOCTYPE html>
<html lang="pt-BR" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Plano de Estudos - DPE Desenvolvedor de Software</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#eef2ff',
                            100: '#e0e7ff',
                            500: '#6366f1',
                            600: '#4f46e5',
                            700: '#4338ca',
                            900: '#312e81',
                        }
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Inter Font -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        /* Glassmorphism effects */
        .glass-card {
            background: rgba(15, 23, 42, 0.82);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        .glass-header {
            background: rgba(15, 23, 42, 0.90);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0f172a;
        }
        ::-webkit-scrollbar-thumb {
            background: #334155;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #475569;
        }
        /* Checkbox styling */
        .custom-checkbox:checked {
            background-color: #6366f1;
            border-color: #6366f1;
        }
        .completed-item {
            opacity: 0.65;
            text-decoration: line-through;
        }
        /* Card background section overlays */
        .section-bg {
            background-size: cover;
            background-position: center;
            position: relative;
        }
        .section-bg::before {
            content: '';
            position: absolute;
            inset: 0;
            background: linear-gradient(180deg, rgba(15, 23, 42, 0.93) 0%, rgba(15, 23, 42, 0.88) 100%);
            border-radius: inherit;
            z-index: 0;
        }
        .section-content {
            position: relative;
            z-index: 10;
        }
    </style>
</head>
<body class="bg-slate-950 text-slate-100 min-h-screen flex flex-col antialiased selection:bg-indigo-500 selection:text-white">

    <!-- STICKY TOP HEADER & GLOBAL PROGRESS -->
    <header class="sticky top-0 z-50 glass-header shadow-2xl">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4">
            <div class="flex flex-col md:flex-row md:items-center md:justify-between gap-4">
                <!-- Title & Badge -->
                <div class="flex items-center space-x-3">
                    <div class="p-2.5 bg-indigo-600/30 border border-indigo-500/40 rounded-xl text-indigo-400">
                        <i class="fa-solid fa-code-commit text-2xl"></i>
                    </div>
                    <div>
                        <h1 class="text-xl sm:text-2xl font-extrabold tracking-tight bg-gradient-to-r from-indigo-400 via-purple-300 to-pink-400 bg-clip-text text-transparent">
                            Concurso DPE - Desenvolvedor de Software
                        </h1>
                        <p class="text-xs text-slate-400 flex items-center gap-2">
                            <span><i class="fa-solid fa-clipboard-check text-indigo-400"></i> Rastreador de Conteúdo Editalício</span>
                            <span>•</span>
                            <span id="lastSavedText">Salvo automaticamente</span>
                        </p>
                    </div>
                </div>

                <!-- Global Stats Badge -->
                <div class="flex items-center gap-4 bg-slate-900/80 border border-slate-800 rounded-xl px-4 py-2 self-start md:self-auto">
                    <div class="text-right">
                        <div class="text-xs text-slate-400 font-medium">Progresso Geral</div>
                        <div class="text-lg font-bold text-indigo-400" id="globalStatsText">0 / 0 (0%)</div>
                    </div>
                    <div class="w-12 h-12 relative flex items-center justify-center">
                        <svg class="w-12 h-12 transform -rotate-90">
                            <circle cx="24" cy="24" r="18" stroke="currentColor" stroke-width="4" class="text-slate-800" fill="transparent"/>
                            <circle id="globalCircularProgress" cx="24" cy="24" r="18" stroke="currentColor" stroke-width="4" class="text-indigo-500 transition-all duration-500 ease-out" stroke-dasharray="113.097" stroke-dashoffset="113.097" stroke-linecap="round" fill="transparent"/>
                        </svg>
                        <i class="fa-solid fa-trophy absolute text-xs text-indigo-400"></i>
                    </div>
                </div>
            </div>

            <!-- Global Linear Progress Bar -->
            <div class="mt-4">
                <div class="flex justify-between items-center text-xs text-slate-400 mb-1 font-semibold">
                    <span>COBERTURA TOTAL DO EDITAL</span>
                    <span id="globalPercentText" class="text-indigo-400 font-bold">0%</span>
                </div>
                <div class="w-full bg-slate-800 rounded-full h-3.5 p-0.5 border border-slate-700/50 shadow-inner">
                    <div id="globalProgressBar" class="bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500 h-2.5 rounded-full transition-all duration-500 ease-out shadow-lg shadow-indigo-500/30" style="width: 0%"></div>
                </div>
            </div>
        </div>
    </header>

    <!-- MAIN CONTENT CONTAINERS -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 flex-1 w-full">
        
        <!-- TOOLBAR: SEARCH & FILTERS -->
        <div class="glass-card rounded-2xl p-4 mb-8 flex flex-col md:flex-row gap-4 justify-between items-center shadow-lg">
            <!-- Search Input -->
            <div class="relative w-full md:w-96">
                <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-1/2 transform -translate-y-1/2 text-slate-400"></i>
                <input type="text" id="searchInput" placeholder="Buscar assunto no edital..." class="w-full pl-10 pr-4 py-2 bg-slate-900/90 border border-slate-700 rounded-xl text-sm focus:outline-none focus:border-indigo-500 text-slate-200 placeholder-slate-500 transition">
            </div>

            <!-- Filter Buttons -->
            <div class="flex flex-wrap items-center gap-2 w-full md:w-auto justify-end">
                <button id="filterAll" class="px-3 py-1.5 rounded-lg text-xs font-semibold bg-indigo-600 text-white shadow-sm transition">Todos</button>
                <button id="filterPending" class="px-3 py-1.5 rounded-lg text-xs font-semibold bg-slate-800 hover:bg-slate-700 text-slate-300 transition">Pendentes</button>
                <button id="filterDone" class="px-3 py-1.5 rounded-lg text-xs font-semibold bg-slate-800 hover:bg-slate-700 text-slate-300 transition">Concluídos</button>
                
                <div class="h-5 w-px bg-slate-700 mx-1 hidden sm:block"></div>

                <!-- Global Action Buttons -->
                <button id="btnCheckAll" class="px-3 py-1.5 rounded-lg text-xs font-medium bg-emerald-950/80 hover:bg-emerald-900 border border-emerald-700/50 text-emerald-300 transition flex items-center gap-1.5" title="Marcar todos os assuntos visíveis">
                    <i class="fa-solid fa-check-double"></i> Marcar Todos
                </button>
                <button id="btnUncheckAll" class="px-3 py-1.5 rounded-lg text-xs font-medium bg-rose-950/80 hover:bg-rose-900 border border-rose-700/50 text-rose-300 transition flex items-center gap-1.5" title="Desmarcar todos os assuntos visíveis">
                    <i class="fa-solid fa-rotate-left"></i> Limpar
                </button>
            </div>
        </div>

        <!-- SECTIONS CONTAINER -->
        <div id="sectionsContainer" class="space-y-8">
            <!-- Sections will be rendered dynamically by JavaScript -->
        </div>

        <!-- NO RESULTS MESSAGE -->
        <div id="noResults" class="hidden text-center py-16 glass-card rounded-2xl">
            <i class="fa-solid fa-folder-open text-4xl text-slate-600 mb-3"></i>
            <h3 class="text-lg font-medium text-slate-300">Nenhum assunto encontrado</h3>
            <p class="text-sm text-slate-500 mt-1">Tente buscar por outros termos ou limpar os filtros.</p>
        </div>
    </main>

    <!-- FOOTER -->
    <footer class="border-t border-slate-800 bg-slate-950/80 py-6 mt-12">
        <div class="max-w-7xl mx-auto px-4 text-center text-xs text-slate-500 flex flex-col sm:flex-row justify-between items-center gap-3">
            <div>
                <i class="fa-solid fa-shield-halved text-indigo-400 mr-1"></i> Concurso Público DPE - Cargo: Desenvolvedor de Software
            </div>
            <div>
                Progresso salvo localmente no seu navegador
            </div>
        </div>
    </footer>

    <!-- CONFIRM DIALOG MODAL -->
    <div id="confirmModal" class="fixed inset-0 bg-slate-950/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="glass-card max-w-md w-full p-6 rounded-2xl border border-slate-700 shadow-2xl">
            <h3 class="text-lg font-bold text-slate-100 flex items-center gap-2" id="modalTitle">
                <i class="fa-solid fa-triangle-exclamation text-amber-400"></i> Confirmar ação
            </h3>
            <p class="text-sm text-slate-300 mt-2" id="modalMessage">Deseja realmente prosseguir?</p>
            <div class="flex justify-end gap-3 mt-6">
                <button id="modalCancel" class="px-4 py-2 rounded-xl text-xs font-semibold bg-slate-800 hover:bg-slate-700 text-slate-300 transition">Cancelar</button>
                <button id="modalConfirm" class="px-4 py-2 rounded-xl text-xs font-semibold bg-indigo-600 hover:bg-indigo-500 text-white transition">Confirmar</button>
            </div>
        </div>
    </div>

    <script>
        const SYLLABUS_DATA = [
            {
                id: "eng-soft",
                title: "Processo de Desenvolvimento e Engenharia de Software",
                icon: "fa-diagram-project",
                bgImage: "https://images.unsplash.com/photo-1517694712202-14dd9538aa97?auto=format&fit=crop&w=1200&q=80",
                rawText: "Processo de desenvolvimento de software: CMMI-DEV v2.0; ABNT NBR ISO/IEC/IEEE 12207:2021; MR-MPS-SW versão 2023; UML 2.5; BPMN; métodos ágeis (Scrum, Kanban, XP e similares); engenharia de requisitos; engenharia de software; modelagem e especificação de processos e sistemas; desenvolvimento low-code e no-code; modelagem de dados estruturados, semiestruturados (XML, JSON) e não estruturados; boas práticas de documentação técnica, dicionário de dados e rastreabilidade de requisitos; qualidade de software segundo o modelo ABNT NBR ISO/IEC 25010:2024; tipos de testes de software (funcionais, não funcionais, unitários, de integração, de sistema, de aceitação, de desempenho, de carga, de estresse, de segurança e de usabilidade); gestão da configuração de software; versionamento semântico; revisão de código (code review); Gestão do ciclo de vida e manutenção de aplicações; gestão de débito técnico; homologação e aceite de sistemas; gestão de mudanças e rastreabilidade de requisitos; documentação técnica e gestão do conhecimento"
            },
            {
                id: "gestao-ti",
                title: "Gestão e Governança de TI e Contratações Públicas",
                icon: "fa-handshake-angle",
                bgImage: "https://images.unsplash.com/photo-1454165804606-c3d57bc86b40?auto=format&fit=crop&w=1200&q=80",
                rawText: "PMBOK – 7ª edição; ITIL v4; COBIT 2019; planejamento estratégico de TIC (PETIC, PDTIC); gestão de portfólio de projetos e produtos digitais; gestão de níveis de serviço (SLAs e OLAs); melhoria contínua; gestão financeira de TI (TCO, ROI, CAPEX, OPEX e FinOps); gestão de riscos de TI baseada na ABNT NBR ISO 31000:2023; gestão de contratos e fornecedores de TIC com foco na Lei nº 14.133/2021; critérios de desempenho e conformidade em contratações de TIC; gestão de stakeholders e comunicação; redação técnica e normativa em TIC; conceitos de arquitetura corporativa, alinhamento estratégico entre TIC e negócio, interoperabilidade e padronização de soluções no setor público; fundamentos conceituais de arquitetura corporativa com base no TOGAF; Identificação de necessidades e prospecção de soluções de TIC; análise de viabilidade; elaboração e validação de especificações técnicas, Estudos Técnicos Preliminares (ETP) e Termos de Referência; provas de conceito (PoC); critérios de seleção, homologação e aceite; fiscalização técnica de contratos, fornecedores e níveis de serviço"
            },
            {
                id: "programacao",
                title: "Programação e Algoritmos",
                icon: "fa-code",
                bgImage: "https://images.unsplash.com/photo-1555066931-4365d14bab8c?auto=format&fit=crop&w=1200&q=80",
                rawText: "Conhecimento das linguagens PHP, Python, C, Java e C#; arcabouço de desenvolvimento .NET; fundamentos de programação: sintaxe, estrutura de programas, compilação e execução; tipos primitivos de dados; variáveis, literais e strings; operadores e precedência; estruturas de controle e repetição; definição de classes, interfaces, métodos e atributos; encapsulamento, herança e polimorfismo; packages; sobrecarga e sobrescrita de métodos; tratamento de exceções; acesso a banco de dados; princípios de orientação a objetos e princípios SOLID; testes automatizados unitários e de integração; TDD e BDD; uso de sistemas de controle de versão (Git); fluxos de trabalho colaborativos (GitFlow, pull requests e code review); uso responsável de assistentes de código baseados em inteligência artificial; Automação de processos e tarefas por scripts, APIs, workflows e RPA; integração de automações com sistemas corporativos"
            },
            {
                id: "banco-dados",
                title: "Banco de Dados e Governança de Dados",
                icon: "fa-database",
                bgImage: "https://images.unsplash.com/photo-1544383835-bda2bc66a55d?auto=format&fit=crop&w=1200&q=80",
                rawText: "Modelo entidade-relacionamento; normalização; comandos SQL: DML, DDL e DCL; controle de transações; SQL e PL/SQL; PostgreSQL versões 14 e 15; Oracle 19c; H2 Database; uso de subconsultas, Common Table Expressions (CTEs) e funções analíticas (window functions); conceitos de modelagem dimensional (fatos, dimensões, métricas, esquemas estrela e floco de neve); conceitos de data warehouse, data mart, OLAP e data lake em nível conceitual; bancos de dados NoSQL (documentos, chave-valor, colunas largas e grafos) em nível conceitual; fundamentos de governança e qualidade de dados (integridade, consistência e rastreabilidade); Arquitetura e modelo corporativo de dados; governança, metadados, catálogo e linhagem de dados; dados mestres e de referência; qualidade de dados e data profiling; ETL e ELT; pipelines de dados; cargas completas e incrementais; Change Data Capture (CDC); transformação, validação, integração e orquestração de dados"
            },
            {
                id: "web-mobile",
                title: "Desenvolvimento Web, Mobile e APIs",
                icon: "fa-globe",
                bgImage: "https://images.unsplash.com/photo-1507238691740-187a5b1d37b8?auto=format&fit=crop&w=1200&q=80",
                rawText: "HTML5, CSS3, Bootstrap 5, JavaScript, TypeScript, Python e .NET; frameworks JavaScript (React, React Native, Angular, Node.js, Vue.js ou equivalentes); Web Services REST; XML: criação, declaração, definição de elementos e atributos, e XML Schema; servidores de aplicação e servidores web; ambientes internet, extranet, intranet e portais; desenvolvimento de APIs RESTful; versionamento de APIs; contratos de API (OpenAPI/Swagger); princípios de design de APIs (idempotência, paginação, autenticação e autorização); desenvolvimento responsivo (mobile-first); usabilidade, experiência do usuário (UX) e acessibilidade digital conforme WCAG e ABNT NBR 17225:2025; integração com serviços externos; uso de JSON em integrações e APIs públicas; governança de APIs; Gestão do ciclo de vida e governança de APIs; publicação, consumo, segurança, monitoramento e documentação de APIs e integrações"
            },
            {
                id: "arq-sistemas",
                title: "Arquitetura de Sistemas e Microsserviços",
                icon: "fa-sitemap",
                bgImage: "https://images.unsplash.com/photo-1451187580459-43490279c0fa?auto=format&fit=crop&w=1200&q=80",
                rawText: "Arquiteturas multicamadas, cliente-servidor e objetos distribuídos; conceitos de SOA; arquiteturas orientadas a eventos, filas e mensageria; padrões arquiteturais MVC, DDD (Domain-Driven Design), arquitetura hexagonal e arquiteturas cloud-native; padrões de resiliência: API Gateway, Service Discovery, circuit breaker, retries e timeouts; integração entre sistemas legados e modernos; arquiteturas orientadas a serviços e a microsserviços em ambientes institucionais; Arquiteturas de referência e integração; governança e documentação de arquitetura; interoperabilidade; escalabilidade; processamento síncrono e assíncrono; arquiteturas distribuídas e orientadas a eventos"
            },
            {
                id: "devops-sec",
                title: "DevOps, DevSecOps e Observabilidade",
                icon: "fa-infinity",
                bgImage: "https://images.unsplash.com/photo-1618401471353-b98afee0b2eb?auto=format&fit=crop&w=1200&q=80",
                rawText: "Integração contínua (CI) e entrega contínua (CD); pipelines de build, teste e deploy; infraestrutura como código; automação de testes de regressão; segurança em pipelines (DevSecOps); observabilidade (logs, métricas e traces); monitoramento contínuo de aplicações; containers e imagens; Docker; ambientes em cluster; Kubernetes; ferramentas de orquestração de containers; estratégias de blue/green deployment e canary releases; Gestão de artefatos e dependências; análise automatizada de qualidade e segurança; gestão de segredos; rastreabilidade de build e deploy; rollback e recuperação de implantações; monitoramento e observabilidade de aplicações e serviços distribuídos; correlação de logs; APM; indicadores de disponibilidade, desempenho e confiabilidade"
            },
            {
                id: "so-redes",
                title: "Sistemas Operacionais e Redes de Computadores",
                icon: "fa-network-wired",
                bgImage: "https://images.unsplash.com/photo-1558494949-ef010cbdcc31?auto=format&fit=crop&w=1200&q=80",
                rawText: "Gerenciamento de processos e threads; alocação de CPU; sincronização; deadlocks e starvation; gerenciamento de memória: segmentação, memória virtual e paginação; sistemas de entrada e saída; armazenamento secundário e terciário; Linux (Red Hat e Oracle Linux): comandos; Microsoft Windows (Windows 10, Windows 11, Windows Server 2019 e Windows Server 2022): PowerShell; conceitos de virtualização de servidores; containers em sistemas operacionais; automação de tarefas administrativas; hardening de sistemas operacionais; Tipos e meios de transmissão; elementos de interconexão; arquitetura TCP/IP; IPv4 e IPv6; DNS; protocolos TCP, UDP, IPsec, ARP, SSH, SMTP, HTTP, FTP, LDAP, DNS, DHCP, POP e IMAP; redes sem fio IEEE 802.11n/ac/ax; conceitos de SDN, NFV, VLAN, VXLAN e redes modernas de data center; Serviços e gerenciamento de redes: serviços de e-mail, DNS, DHCP e Web Proxy; servidores de aplicação (JBoss, Apache HTTP Server, IIS); análise de desempenho de redes; VPNs corporativas; acesso remoto seguro; QoS para voz, vídeo e dados; SNMP, agentes, gerentes e MIBs; níveis de serviço e métricas de desempenho; métodos de avaliação de desempenho; ferramentas de monitoramento e logs: Zabbix, Elasticsearch, Logstash, Kibana, Grafana, Prometheus e Fluentd"
            },
            {
                id: "seguranca",
                title: "Segurança da Informação e Proteção de Dados",
                icon: "fa-shield-halved",
                bgImage: "https://images.unsplash.com/photo-1563986768609-322da13575f3?auto=format&fit=crop&w=1200&q=80",
                rawText: "ABNT NBR ISO/IEC 27001:2024 e ABNT NBR ISO/IEC 27002:2022; sistemas de proteção: firewall, WAF, UTM, DMZ, proxy, NAC, antivírus e antispam; IDS e IPS; monitoramento de tráfego; segurança em redes sem fio (EAP, WPA, WPA2 e WPA3); VPN, VPN-SSL e ZTNA; ataques e ameaças: malware, DoS e DDoS; criptografia simétrica e assimétrica; certificados e assinaturas digitais; hashes criptográficos; controle de acesso: autenticação, autorização e auditoria; RBAC e MFA; SSL/TLS; Lei Geral de Proteção de Dados Pessoais – LGPD (Lei nº 13.709/2018): fundamentos, princípios, bases legais, tratamento pelo Poder Público, direitos dos titulares, agentes de tratamento e papel da ANPD; anonimização e pseudonimização; gestão de riscos de segurança segundo ABNT NBR ISO/IEC 27005:2023; gestão de incidentes conforme ISO/IEC 27035-1:2023 e NIST SP 800-61; segurança em nuvem conforme NBR ISO/IEC 27017:2016; defesa em profundidade; Zero Trust; SOC, SIEM, EDR e segurança de endpoints; gestão e correlação de logs; segurança de APIs e aplicações web conforme OWASP Top 10:2025; IAM, SSO, OAuth 2.0 e OpenID Connect (OIDC); Segurança no ciclo de vida de desenvolvimento (SSDLC); secure by design e secure by default; modelagem de ameaças; análise de segurança de aplicações (SAST e DAST); gestão de vulnerabilidades, dependências e segredos; segurança de containers; proteção de dados em repouso e em trânsito"
            },
            {
                id: "nuvem-ia",
                title: "Computação em Nuvem, Big Data, Analytics e IA",
                icon: "fa-brain",
                bgImage: "https://images.unsplash.com/photo-1677442136019-21780efad99a?auto=format&fit=crop&w=1200&q=80",
                rawText: "Conceitos de nuvem pública, privada, híbrida e multicloud; modelos de serviço IaaS, PaaS e SaaS; estratégias de migração de aplicações; governança de nuvem; controle de custos; escalabilidade; alta disponibilidade e resiliência; uso de serviços gerenciados de banco de dados, mensageria, armazenamento e integração; Arquiteturas de dados e processamento distribuído em nuvem; serviços batch e streaming; integração de soluções de dados e inteligência artificial; governança e observabilidade de aplicações cloud-native; Engenharia de Dados, Processamento Massivo de Dados e Analytics: fundamentos de engenharia e arquitetura de dados; Big Data; processamento distribuído, batch e streaming; escalabilidade e tolerância a falhas; pipelines e orquestração de dados; Apache Spark, Apache Kafka ou tecnologias equivalentes; integração entre data lake, data warehouse e sistemas transacionais; data lakehouse em nível conceitual; Business Intelligence e apoio à decisão: fundamentos e arquitetura de BI; indicadores, métricas e KPIs; construção de dashboards e relatórios analíticos; visualização de dados; análise multidimensional e OLAP; integração de ferramentas de BI com data warehouses, data marts, APIs e outras fontes de dados; disponibilização de informações para apoio à tomada de decisões; Inteligência Artificial e Automação Inteligente: fundamentos de inteligência artificial e aprendizado de máquina; aprendizagem supervisionada e não supervisionada; treinamento, validação e avaliação de modelos; redes neurais e deep learning em nível conceitual; inteligência artificial generativa e Large Language Models (LLMs); embeddings, busca semântica, bancos vetoriais e RAG; prompt engineering; integração de modelos de IA com aplicações e APIs; agentes de IA; avaliação, segurança, privacidade, explicabilidade, vieses, governança e uso responsável de IA; fundamentos de MLOps; automação de processos com workflows, APIs, RPA e inteligência artificial"
            },
            {
                id: "pdpj-br",
                title: "Plataforma Digital do Poder Judiciário (PDPJ-Br) e Normativos",
                icon: "fa-scale-balanced",
                bgImage: "https://images.unsplash.com/photo-1589829545856-d10d557cf95f?auto=format&fit=crop&w=1200&q=80",
                rawText: "Normativos da Plataforma Digital do Poder Judiciário (PDPJ-Br): Plataforma Digital do Poder Judiciário Brasileiro – objetivos, princípios, governança, interoperabilidade, padronização e integração entre sistemas judiciais; Resoluções CNJ nº 522/2023 (MoReq-Jus), nº 396/2021 e nº 335/2020; Portarias CNJ nº 252/2020, nº 253/2020, nº 284/2021, nº 131/2021 e nº 162/2021; Arquitetura de desenvolvimento da Plataforma Digital do Poder Judiciário (PDPJ-Br): linguagem de programação Java; arquitetura distribuída baseada em microsserviços; APIs RESTful; JSON; Spring Framework, Spring Boot e Spring Cloud; Service Discovery; Eureka; Zuul e API Gateway; MapStruct; Swagger; persistência de dados com JPA 2.0, Hibernate 4.3 ou superior e Hibernate Envers; controle de versão de banco de dados com Flyway; bancos de dados PostgreSQL e H2 Database; autenticação e autorização com SSO, Keycloak e OAuth2 (RFC 6749); mensageria e integração com Message Broker, RabbitMQ, eventos negociais, Webhooks e APIs reversas; versionamento de código com Git; ambientes em cluster com Kubernetes; orquestração de containers com Rancher; deploy de aplicações; integração contínua e entrega contínua (CI/CD)"
            },
            {
                id: "ingles",
                title: "Inglês Técnico",
                icon: "fa-language",
                bgImage: "https://images.unsplash.com/photo-1456513080510-7bf3a84b82f8?auto=format&fit=crop&w=1200&q=80",
                rawText: "Inglês técnico: leitura, compreensão e interpretação de documentação técnica em TI, manuais, especificações arquiteturais, APIs e termos tecnológicos"
            }
        ];

        const STORAGE_KEY = "DPE_DEV_STUDY_PROGRESS_V1";
        let userState = loadState();
        let currentFilter = 'all'; // 'all', 'pending', 'done'
        let searchQuery = '';

        function loadState() {
            try {
                const saved = localStorage.getItem(STORAGE_KEY);
                return saved ? JSON.parse(saved) : {};
            } catch (e) {
                console.error("Erro ao carregar do localStorage", e);
                return {};
            }
        }

        function saveState() {
            try {
                localStorage.setItem(STORAGE_KEY, JSON.stringify(userState));
                const lastSavedEl = document.getElementById("lastSavedText");
                if (lastSavedEl) {
                    const now = new Date();
                    lastSavedEl.textContent = `Salvo às ${now.toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'})}`;
                }
            } catch (e) {
                console.error("Erro ao salvar no localStorage", e);
            }
        }

        // Parses semicolon-separated text into structured items
        function parseTopics(rawText, sectionId) {
            return rawText
                .split(';')
                .map(item => item.trim())
                .filter(item => item.length > 0)
                .map((text, idx) => {
                    // Clean redundant newlines or leading spaces
                    const cleaned = text.replace(/\s+/g, ' ');
                    const id = `${sectionId}_item_${idx}`;
                    return { id, text: cleaned };
                });
        }

        function renderSyllabus() {
            const container = document.getElementById('sectionsContainer');
            container.innerHTML = '';

            let totalItemsCount = 0;
            let totalCheckedCount = 0;
            let visibleSections = 0;

            SYLLABUS_DATA.forEach(section => {
                const items = parseTopics(section.rawText, section.id);
                
                // Filter items according to search and status filter
                const filteredItems = items.filter(item => {
                    const matchesSearch = searchQuery === '' || item.text.toLowerCase().includes(searchQuery.toLowerCase());
                    const isChecked = !!userState[item.id];
                    
                    let matchesFilter = true;
                    if (currentFilter === 'pending') matchesFilter = !isChecked;
                    if (currentFilter === 'done') matchesFilter = isChecked;

                    return matchesSearch && matchesFilter;
                });

                // Calculate section stats based on ALL items in the section
                const sectionCheckedCount = items.filter(item => !!userState[item.id]).length;
                const sectionPercent = items.length > 0 ? Math.round((sectionCheckedCount / items.length) * 100) : 0;

                totalItemsCount += items.length;
                totalCheckedCount += sectionCheckedCount;

                // Don't render empty sections during active filtering/search if no items match
                if (filteredItems.length === 0 && (searchQuery !== '' || currentFilter !== 'all')) {
                    return;
                }

                visibleSections++;

                // Build Section HTML Card with Background Image
                const sectionCard = document.createElement('div');
                sectionCard.className = 'section-bg glass-card rounded-2xl shadow-xl overflow-hidden transition-all duration-300 border border-slate-800 hover:border-slate-700';
                sectionCard.style.backgroundImage = `url('${section.bgImage}')`;

                let itemsHTML = '';
                filteredItems.forEach(item => {
                    const isChecked = !!userState[item.id];
                    itemsHTML += `
                        <label for="${item.id}" class="group flex items-start gap-3 p-3 rounded-xl bg-slate-900/60 hover:bg-slate-900/90 border border-slate-800/80 hover:border-indigo-500/30 transition cursor-pointer selection:bg-none">
                            <div class="flex items-center h-5 mt-0.5">
                                <input type="checkbox" id="${item.id}" data-item-id="${item.id}" ${isChecked ? 'checked' : ''} 
                                       class="custom-checkbox w-4 h-4 rounded border-slate-700 text-indigo-600 focus:ring-indigo-500 focus:ring-offset-slate-900 cursor-pointer transition">
                            </div>
                            <div class="text-sm text-slate-300 group-hover:text-slate-100 transition leading-snug ${isChecked ? 'completed-item text-slate-500' : ''}">
                                ${escapeHTML(item.text)}
                            </div>
                        </label>
                    `;
                });

                sectionCard.innerHTML = `
                    <div class="section-content p-6">
                        <!-- Section Header -->
                        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 mb-4 pb-4 border-b border-slate-800/80">
                            <div class="flex items-center gap-3">
                                <div class="w-10 h-10 rounded-xl bg-indigo-600/20 border border-indigo-500/30 flex items-center justify-center text-indigo-400">
                                    <i class="fa-solid ${section.icon} text-lg"></i>
                                </div>
                                <div>
                                    <h2 class="text-lg font-bold text-slate-100 tracking-wide">${section.title}</h2>
                                    <span class="text-xs text-slate-400 font-medium">${items.length} tópicos descritos</span>
                                </div>
                            </div>
                            
                            <!-- Section Progress Indicator -->
                            <div class="flex items-center gap-3 bg-slate-950/80 border border-slate-800 px-3.5 py-1.5 rounded-xl self-start sm:self-auto">
                                <div class="text-right">
                                    <div class="text-[10px] uppercase tracking-wider font-semibold text-slate-400">Concluído</div>
                                    <div class="text-xs font-bold text-indigo-400">${sectionCheckedCount} de ${items.length} (${sectionPercent}%)</div>
                                </div>
                                <div class="w-8 h-8 relative flex items-center justify-center">
                                    <svg class="w-8 h-8 transform -rotate-90">
                                        <circle cx="16" cy="16" r="12" stroke="currentColor" stroke-width="3" class="text-slate-800" fill="transparent"/>
                                        <circle cx="16" cy="16" r="12" stroke="currentColor" stroke-width="3" class="text-indigo-400" stroke-dasharray="75.398" stroke-dashoffset="${75.398 - (75.398 * sectionPercent) / 100}" stroke-linecap="round" fill="transparent"/>
                                    </svg>
                                </div>
                            </div>
                        </div>

                        <!-- Section Progress Bar -->
                        <div class="mb-5">
                            <div class="w-full bg-slate-950/80 rounded-full h-2.5 p-0.5 border border-slate-800">
                                <div class="bg-gradient-to-r from-indigo-500 to-purple-500 h-1.5 rounded-full transition-all duration-300" style="width: ${sectionPercent}%"></div>
                            </div>
                        </div>

                        <!-- Topic Items Grid -->
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-2.5">
                            ${itemsHTML || '<p class="text-xs text-slate-500 italic py-2 col-span-2">Nenhum item corresponde aos filtros selecionados nesta seção.</p>'}
                        </div>
                    </div>
                `;

                container.appendChild(sectionCard);
            });

            // Handle "No Results" display
            const noResults = document.getElementById('noResults');
            if (visibleSections === 0) {
                noResults.classList.remove('hidden');
            } else {
                noResults.classList.add('hidden');
            }

            // Update Overall Progress Indicators
            updateGlobalStats(totalCheckedCount, totalItemsCount);
        }

        function updateGlobalStats(checked, total) {
            const overallPercent = total > 0 ? Math.round((checked / total) * 100) : 0;
            
            document.getElementById('globalStatsText').textContent = `${checked} / ${total} (${overallPercent}%)`;
            document.getElementById('globalPercentText').textContent = `${overallPercent}%`;
            document.getElementById('globalProgressBar').style.width = `${overallPercent}%`;

            const circular = document.getElementById('globalCircularProgress');
            if (circular) {
                const circumference = 113.097;
                const offset = circumference - (circumference * overallPercent) / 100;
                circular.style.strokeDashoffset = offset;
            }
        }

        function escapeHTML(str) {
            return str.replace(/[&<>'"]/g, 
                tag => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', "'": '&#39;', '"': '&quot;' }[tag] || tag)
            );
        }

        document.addEventListener('DOMContentLoaded', () => {
            renderSyllabus();

            // Delegate Checkbox Change Events
            document.getElementById('sectionsContainer').addEventListener('change', (e) => {
                if (e.target && e.target.matches('input[type="checkbox"]')) {
                    const itemId = e.target.getAttribute('data-item-id');
                    userState[itemId] = e.target.checked;
                    saveState();
                    renderSyllabus();
                }
            });

            // Search Input Event
            const searchInput = document.getElementById('searchInput');
            searchInput.addEventListener('input', (e) => {
                searchQuery = e.target.value;
                renderSyllabus();
            });

            // Filter Buttons Event Listeners
            const btnAll = document.getElementById('filterAll');
            const btnPending = document.getElementById('filterPending');
            const btnDone = document.getElementById('filterDone');

            function setActiveFilterBtn(activeBtn) {
                [btnAll, btnPending, btnDone].forEach(btn => {
                    btn.className = "px-3 py-1.5 rounded-lg text-xs font-semibold bg-slate-800 hover:bg-slate-700 text-slate-300 transition";
                });
                activeBtn.className = "px-3 py-1.5 rounded-lg text-xs font-semibold bg-indigo-600 text-white shadow-sm transition";
            }

            btnAll.addEventListener('click', () => {
                currentFilter = 'all';
                setActiveFilterBtn(btnAll);
                renderSyllabus();
            });

            btnPending.addEventListener('click', () => {
                currentFilter = 'pending';
                setActiveFilterBtn(btnPending);
                renderSyllabus();
            });

            btnDone.addEventListener('click', () => {
                currentFilter = 'done';
                setActiveFilterBtn(btnDone);
                renderSyllabus();
            });

            // Batch Actions (Marcar Todos / Limpar)
            document.getElementById('btnCheckAll').addEventListener('click', () => {
                showModal(
                    "Marcar todos os assuntos?", 
                    "Isso vai marcar como estudado todos os tópicos das disciplinas apresentadas.",
                    () => {
                        SYLLABUS_DATA.forEach(section => {
                            const items = parseTopics(section.rawText, section.id);
                            items.forEach(item => {
                                userState[item.id] = true;
                            });
                        });
                        saveState();
                        renderSyllabus();
                    }
                );
            });

            document.getElementById('btnUncheckAll').addEventListener('click', () => {
                showModal(
                    "Limpar progresso?", 
                    "Isso vai desmarcar todos os assuntos estudados. Esta ação pode ser refeita marcando-os novamente.",
                    () => {
                        userState = {};
                        saveState();
                        renderSyllabus();
                    }
                );
            });
        });

        function showModal(title, message, onConfirm) {
            const modal = document.getElementById('confirmModal');
            document.getElementById('modalTitle').innerHTML = `<i class="fa-solid fa-triangle-exclamation text-amber-400"></i> ${title}`;
            document.getElementById('modalMessage').textContent = message;

            modal.classList.remove('hidden');

            const btnConfirm = document.getElementById('modalConfirm');
            const btnCancel = document.getElementById('modalCancel');

            const cleanup = () => {
                modal.classList.add('hidden');
                btnConfirm.removeEventListener('click', handleConfirm);
                btnCancel.removeEventListener('click', handleCancel);
            };

            const handleConfirm = () => {
                onConfirm();
                cleanup();
            };

            const handleCancel = () => {
                cleanup();
            };

            btnConfirm.addEventListener('click', handleConfirm);
            btnCancel.addEventListener('click', handleCancel);
        }
    </script>
</body>
</html>

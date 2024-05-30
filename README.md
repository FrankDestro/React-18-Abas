# React-18-Abas

### React Component 

```java
import React, { useState } from 'react';
import { Button, Tab, Table, Tabs } from 'react-bootstrap';

import { faList, faPlus } from '@fortawesome/free-solid-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
import './styles.css';

interface Chamado {
    id: number;
    title: string;
    description: string;
}

const Abas: React.FC = () => {
    const [activeKey, setActiveKey] = useState<string | undefined>("1");
    const [openTabs, setOpenTabs] = useState<Array<{ key: string, chamado: Chamado | null }>>([
        { key: "1", chamado: null }
    ]);

    const chamados: Chamado[] = [
        { id: 1, title: "Chamado 1", description: "Descrição do Chamado 1" },
        { id: 2, title: "Chamado 2", description: "Descrição do Chamado 2" },
        { id: 3, title: "Chamado 3", description: "Descrição do Chamado 3" }
    ];

    const handleSelect = (key: string | null) => {
        if (key) {
            setActiveKey(key);
        }
    };

    const handleChamadoClick = (chamado: Chamado) => {
        const existingTab = openTabs.find(tab => tab.chamado && tab.chamado.id === chamado.id);
        if (existingTab) {
            setActiveKey(existingTab.key);
        } else {
            const newKey = `chamado-${chamado.id}`;
            setOpenTabs([...openTabs, { key: newKey, chamado }]);
            setActiveKey(newKey);
        }
    };

    const handleCloseTab = (key: string) => {
        const filteredTabs = openTabs.filter(tab => tab.key !== key);
        setOpenTabs(filteredTabs);
        if (activeKey === key) {
            setActiveKey(filteredTabs.length > 0 ? filteredTabs[0].key : "1");
        }
    };

    return (
        <div className='container-table-abas'>
            <Tabs activeKey={activeKey} onSelect={handleSelect} className='content-table'>
                <Tab eventKey="1"
                    title={
                        <>
                            <FontAwesomeIcon icon={faList} />
                            <span style={{ marginLeft: "10px" }}>Tickets</span>
                        </>
                    }
                >
                    <Table striped bordered hover>
                        <thead>
                            <tr>
                                <th>ID</th>
                                <th>Título</th>
                            </tr>
                        </thead>
                        <tbody>
                            {chamados.map(chamado => (
                                <tr key={chamado.id} onClick={() => handleChamadoClick(chamado)}>
                                    <td>{chamado.id} </td>
                                    <td>{chamado.title}</td>
                                </tr>
                            ))}
                        </tbody>
                    </Table>
                </Tab>
                {openTabs.map(tab => tab.key !== "1" && (
                    <Tab key={tab.key} eventKey={tab.key}
                        title={
                            <>
                                <div className='container-title-tab'>
                                    <div>
                                        {tab.chamado?.title}
                                    </div>
                                    <div className="close-icon" >
                                        <span onClick={() => handleCloseTab(tab.key)} className='close-title-icon'>X</span>
                                    </div>
                                </div>
                            </>
                        }>
                        <div>
                            {tab.chamado && (
                                <>
                                    <h3>{tab.chamado.title}</h3>
                                    <p>{tab.chamado.description}</p>
                                    <Button variant="danger" onClick={() => handleCloseTab(tab.key)}>Fechar</Button>
                                </>
                            )}
                        </div>
                    </Tab>
                ))}
                <Tab eventKey="novo-chamado"
                    title={
                        <>
                            <FontAwesomeIcon icon={faPlus} />
                            <span style={{ marginLeft: "10px" }}>Novo Ticket</span>
                        </>
                    }>
                    <div>
                        <h3>Abra um Novo Chamado</h3>
                        <p>Formulário para abrir um novo chamado vai aqui.</p>
                        {/* Adicione o formulário de novo chamado aqui */}
                    </div>
                </Tab>
            </Tabs>
        </div>
    );
};

export default Abas;

```

### Styles CSS

```css
.container-table-abas {
    margin: 10px;
}

.nav-tabs .nav-link.active {
    background-color: #007bffb9;
    color: #fff;
}

.nav-tabs .nav-link {
    color: #000;
}

.nav-tabs .nav-link:hover {
    border-color: rgb(112, 112, 112);
}

.container-title-tab {
    display: flex;
    justify-content: space-between;
    width: 100%;
}

.close-icon span {
    margin-left: 8px;
    font-size: 15px;
    font-weight: 700;
}

.close-icon span:hover {
   color: rgb(184, 58, 54);
}

.nav-link {
    width: 160px;
}

.nav-item {
    border: 1px solid rgba(117, 115, 115, 0.26);
    border-top-left-radius: 7px;
    border-top-right-radius: 7px;
}


```

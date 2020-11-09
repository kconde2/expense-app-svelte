<script>
    import {
        Form,
        FormGroup,
        Input,
        Label,
        Button,
        Col,
        Row,
        Container,
    } from "sveltestrap";

    let persons = [
        {
            id: "souad",
            text: `Soutou`,
        },
        {
            id: "kaba",
            text: `KFC`,
        },
    ];

    let frequencies = [
        {
            id: "dayly",
            text: `Journalier`,
        },
        {
            id: "monthly",
            text: `Mensuel`,
        },
        {
            id: "yearly",
            text: `Annuel`,
        },
    ];

    let form = {
        who: "",
        amount: 0,
        entitled: "",
        date: null,
        frequency: "",
    };

    function handleSubmit() {
        alert(
            `answered question ${selected.id} (${selected.text}) with "${answer}"`
        );
    }

    function filled() {
        return (
            form.entitled !== "" &&
            form.amount !== 0 &&
            form.date !== null &&
            persons.filter((e) => e.id === form.who).length > 0 &&
            frequencies.filter((e) => e.id === form.frequency).length > 0
        );
    }
</script>

<Container>
    <Row>
        <Col>
            <Form on:submit.preventDefault()={handleSubmit}>
                <FormGroup>
                    <Label for="who">Qui a effectué la dépense ?</Label>
                    <Input
                        type="select"
                        name="select"
                        id="who"
                        bind:value={form.person}>
                        {#each persons as person}
                            <option value={person}>{person.text}</option>
                        {/each}
                    </Input>
                </FormGroup>

                <FormGroup>
                    <Label for="amount">Montant</Label>
                    <Input
                        type="number"
                        id="amount"
                        placeholder="Montant"
                        required
                        bind:value={form.amount} />
                </FormGroup>

                <FormGroup>
                    <Label for="entitled">Libellé</Label>
                    <Input
                        type="text"
                        id="entitled"
                        placeholder="Libellé"
                        required
                        bind:value={form.entitled} />
                </FormGroup>

                <FormGroup>
                    <Label for="frequency">Fréquence</Label>
                    <Input
                        type="select"
                        name="select"
                        id="frequency"
                        required
                        bind:value={form.frequency}>
                        {#each frequencies as frequency}
                            <option value={frequency}>{frequency.text}</option>
                        {/each}
                    </Input>
                </FormGroup>

                <FormGroup>
                    <Label for="expenseDate">Date</Label>
                    <Input
                        type="date"
                        name="date"
                        id="expenseDate"
                        placeholder="Date"
                        required
                        bind:value={form.date} />
                </FormGroup>

                <Button color="primary" disabled={!filled} type="submit">
                    Enregistrer
                </Button>
            </Form>
        </Col>
    </Row>
</Container>

# React Bootstrap

## Table of Contents
1. [Introduction](#1-introduction)
2. [Installation](#2-installation)
3. [Using Components](#3-using-components)
4. [Grid System](#4-grid-system)
5. [Practical Example](#5-practical-example)
6. [Quick Reference](#6-quick-reference)
7. [Interview Questions](#7-interview-questions)

---

## 1. Introduction

### 1.1 What is React Bootstrap?
**React-Bootstrap** replaces the Bootstrap JavaScript defined in standard Bootstrap with React components. It relies entirely on the Bootstrap stylesheet but does not use jQuery or Bootstrap's JavaScript (popper.js etc.) for behavior.

---

## 2. Installation

```bash
npm install react-bootstrap bootstrap
```

**Import CSS:**
In `main.jsx` or `App.jsx`, import the CSS file:
```javascript
import 'bootstrap/dist/css/bootstrap.min.css';
```

---

## 3. Using Components

You strictly import the components you need.

```jsx
import Button from 'react-bootstrap/Button';
import Alert from 'react-bootstrap/Alert';

function MyComponent() {
  return (
    <>
      <Alert variant="primary">This is a Bootstrap Alert!</Alert>
      <Button variant="success">Click Me</Button>
    </>
  );
}
```

---

## 4. Grid System

React Bootstrap converts the familiar Bootstrap grid (`row`, `col`) into components: `<Container>`, `<Row>`, `<Col>`.

```jsx
import Container from 'react-bootstrap/Container';
import Row from 'react-bootstrap/Row';
import Col from 'react-bootstrap/Col';

function GridExample() {
  return (
    <Container>
      <Row>
        <Col sm={8}>sm=8 (Takes 8/12 width)</Col>
        <Col sm={4}>sm=4 (Takes 4/12 width)</Col>
      </Row>
      <Row>
        <Col>Auto Layout 1</Col>
        <Col>Auto Layout 2</Col>
        <Col>Auto Layout 3</Col>
      </Row>
    </Container>
  );
}
```

---

## 5. Practical Example

### 5.1 Navbar and Card
(Based on `Header.jsx` from `reactcrud` project)

```jsx
import Button from 'react-bootstrap/Button';
import Container from 'react-bootstrap/Container';
import Form from 'react-bootstrap/Form';
import Nav from 'react-bootstrap/Nav';
import Navbar from 'react-bootstrap/Navbar';

function MyHeader() {
  return (
    <Navbar expand="lg" className="bg-body-tertiary">
      <Container fluid>
        <Navbar.Brand href="#">My App</Navbar.Brand>
        <Navbar.Toggle aria-controls="navbarScroll" />
        <Navbar.Collapse id="navbarScroll">
          <Nav className="me-auto">
            <Nav.Link href="#home">Home</Nav.Link>
            <Nav.Link href="#link">Link</Nav.Link>
          </Nav>
          <Form className="d-flex">
            <Form.Control
              type="search"
              placeholder="Search"
              className="me-2"
              aria-label="Search"
            />
            <Button variant="outline-success">Search</Button>
          </Form>
        </Navbar.Collapse>
      </Container>
    </Navbar>
  );
}
```

---

## 6. Quick Reference

| Component | Usage |
|-----------|-------|
| `<Button>` | `variant="primary|danger|success"` |
| `<Alert>` | `variant="info|warning"` |
| `<Container>` | `fluid` (full width) or default |
| `<Row>/<Col>` | Grid system layout |
| `<Card>` | Container for content with header/body |
| `<Modal>` | Popup dialogs |

---

## 7. Interview Questions

### Q1: Why use React Bootstrap instead of standard Bootstrap?
**Answer**:
1. **Component-Based**: Fits perfectly into the React ecosystem.
2. **No jQuery**: Removes the heavy jQuery dependency, improving performance and avoiding conflicts with React's Virtual DOM.
3. **Cleaner JSX**: Use `<Col xs={6}>` instead of `<div className="col-xs-6">`.

### Q2: How do you include Bootstrap CSS in React?
**Answer**: Install the `bootstrap` npm package and import the CSS file (`import 'bootstrap/dist/css/bootstrap.min.css'`) in your entry file (`main.jsx` or `App.jsx`).

---

## Navigation

← Previous: [56_Redux_Demo_and_Practice.md](./56_Redux_Demo_and_Practice.md) | Next: [58_jQuery_Introduction.md](../Module_08_jQuery/58_jQuery_Introduction.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 11*

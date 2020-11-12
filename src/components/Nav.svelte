<script>
    import {
      Collapse,
      Navbar,
      NavbarToggler,
      NavbarBrand,
      Nav,
      NavItem,
      NavLink,
    } from 'sveltestrap';
  
    let isOpen = false;
  
    function handleUpdate(event) {
      isOpen = event.detail.isOpen;
    }
  </script>
  
  <Navbar color="dark" dark expand="md">
    <NavbarBrand href="/">IoT Project</NavbarBrand>
    <NavbarToggler on:click={() => (isOpen = !isOpen)} />
    <Collapse {isOpen} navbar expand="md" on:update={handleUpdate}>
      <Nav navbar>
        <NavItem>
          <NavLink href="#Charts/">Charts</NavLink>
        </NavItem>
        <NavItem>
          <NavLink href="#About/">About</NavLink>
        </NavItem>
      </Nav>
    </Collapse>
  </Navbar>